---
name: ship-ios-to-testflight-keyonly
description: Build and upload an iOS or macOS Catalyst app to TestFlight using only an App Store Connect API key — no manual App Store Connect clicking, no interactive Apple ID login, fully headless / CI-able.
---

# Ship iOS + macOS to TestFlight with an ASC API key only

## What this is

A fastlane setup that builds, signs, and uploads an iOS (and macOS Catalyst) app to
TestFlight with **one credential**: an App Store Connect API key (`.p8`). No interactive
Apple ID login, no portal clicking for signing, no certs to restore on a fresh machine.
The key mints the distribution cert and provisioning profile on demand, so a brand-new CI
runner needs nothing but the `.p8`, the key ID, and the issuer ID.

## When to use

- Headless CI/CD where you cannot do a browser-based Apple Sign-In.
- A fresh machine with no signing assets restored.
- You want store metadata + screenshots reproducible from versioned files, not hand-typed.
- Works for native Xcode projects, Expo (`expo prebuild`), and Capacitor (`npx cap sync ios`).

## Prerequisites

- An App Store Connect API key with **App Manager / Admin** role. Three values:
  `key_id`, `issuer_id`, and the `.p8` file (keep it gitignored, never commit it).
- Xcode + `fastlane` installed. A `Release` scheme that archives.
- Automatic signing left on in the target (`CODE_SIGN_STYLE=Automatic`).
- The app record already exists in App Store Connect (see "The one manual gate").

## The procedure

All lanes call `app_store_connect_api_key(...)` **first** — it stuffs the token into the
lane context (`Spaceship::ConnectAPI`), which is how `produce`, `upload_to_testflight`,
and `deliver` authenticate without a login. They have no `api_key` of their own to pass it.

1. **Register the app record (first run only).**
   `produce` with `skip_devcenter: true`. This creates *only* the App Store Connect
   record via the token-auth API. We skip the Developer-Portal half because that uses
   legacy Apple-ID web login the key can't satisfy — and we don't need it: the App ID in
   the portal gets auto-created by `xcodebuild -allowProvisioningUpdates` during the build.

2. **Build + upload to TestFlight (`:beta`).**
   `build_app` is the one action with **no `api_key` param**, so auth is threaded through
   `xcargs` instead:
   ```
   xcargs: "DEVELOPMENT_TEAM=YOUR_TEAM_ID CODE_SIGN_STYLE=Automatic " \
           "-allowProvisioningUpdates " \
           "-authenticationKeyID YOUR_KEY_ID " \
           "-authenticationKeyIssuerID YOUR_ISSUER_ID " \
           "-authenticationKeyPath #{absolute_path_to_p8}"
   ```
   The `-authenticationKeyPath` **must be absolute** — relative paths silently fail to
   authenticate. `File.expand_path("../keys/AuthKey_XXXX.p8", __dir__)` from the Fastfile.
   Then `upload_to_testflight(api_key: api_key, skip_waiting_for_build_processing: true)`.

3. **Push metadata (`:metadata`).**
   `upload_to_app_store` with `skip_binary_upload: true, skip_screenshots: true,
   force: true`. Fields live in `fastlane/metadata/`. `force: true` suppresses the
   interactive HTML preview so it runs unattended.

4. **Push screenshots (`:screenshots`).**
   `upload_to_app_store` with `skip_binary_upload: true, skip_metadata: true,
   overwrite_screenshots: true, force: true`, reading from `fastlane/screenshots/`.

5. **macOS Catalyst build (`:mac`).**
   Same as `:beta` plus `catalyst_platform: "macos"` in `build_app` and
   `app_platform: "osx"` in `upload_to_testflight`. With `SUPPORTS_MACCATALYST=YES` and
   `DERIVE_MACCATALYST_PRODUCT_BUNDLE_IDENTIFIER=NO` in the target, the Mac build shares
   the **same bundle id and ASC record** as iOS (Universal Purchase) — no separate record.

6. **macOS screenshots (`:mac_screenshots`).**
   `upload_to_app_store(platform: "osx", screenshots_path: "./fastlane/screenshots-mac")`.
   Catalyst screenshots are **2880×1800**; deliver auto-maps that size to the
   `APP_DESKTOP` display type — you don't name the display type yourself.

7. **Mint the Mac installer cert key-only (`:mac_cert`), if uploading a Catalyst build.**
   The ASC API *can* create certificates (`POST /v1/certificates`), so
   `cert(platform: "macos", type: "mac_installer_distribution", api_key: api_key)`
   generates the CSR, creates + downloads the cert, and imports it to the keychain — no
   portal click. Idempotent: reuses an existing valid cert.

## Gotchas & failure modes

- **`app_store_connect_api_key` must run first**, in every lane. If `produce`/`deliver`/
  `pilot` prompts for an Apple ID, you forgot it or it ran after.
- **`build_app` has no `api_key`** — authenticate via `xcargs -authenticationKey*`. Easy to
  pass the key everywhere *except* the build and then wonder why signing prompts for login.
- **`-authenticationKeyPath` must be ABSOLUTE.** Relative path = silent auth failure.
- **`produce` without `skip_devcenter: true`** falls back to legacy web login (Apple ID +
  password) for the portal half → forces an interactive login. Always skip devcenter.
- **Expo / Capacitor regenerate the project** (`expo prebuild --clean`,
  `npx cap sync ios`) and wipe signing build settings — that's exactly why
  `DEVELOPMENT_TEAM` + `CODE_SIGN_STYLE` go through `xcargs`, not the project file. For
  Capacitor: run the web build + `npx cap sync ios` **before** the lane.
- **Reused build number** is auto-rejected by TestFlight. Keep the build number ahead of
  the latest processed build; bump it before every upload.
- **`force: true` is required** on `upload_to_app_store` for unattended runs, or it opens
  an HTML preview and blocks waiting for a human.

## The one manual gate

Honest caveat: the **very first creation of the App Store Connect app record** can require
a one-time interactive web session in some Apple accounts (`produce` via the key works for
many, but Apple occasionally gates brand-new record creation behind a logged-in session).
After the record exists, everything above is fully key-only and headless forever. Treat it
like a one-time account bootstrap, the same shape as the first Catalyst installer cert.

## Minimal example

```ruby
lane :beta do
  api_key = app_store_connect_api_key(
    key_id: "YOUR_KEY_ID", issuer_id: "YOUR_ISSUER_ID",
    key_filepath: "keys/AuthKey_XXXX.p8",
  )
  auth_key_path = File.expand_path("../keys/AuthKey_XXXX.p8", __dir__)

  build_app(
    workspace: "ios/App.xcworkspace", scheme: "App", configuration: "Release",
    export_method: "app-store",
    export_options: { signingStyle: "automatic", teamID: "YOUR_TEAM_ID" },
    xcargs: "DEVELOPMENT_TEAM=YOUR_TEAM_ID CODE_SIGN_STYLE=Automatic " \
            "-allowProvisioningUpdates " \
            "-authenticationKeyID YOUR_KEY_ID " \
            "-authenticationKeyIssuerID YOUR_ISSUER_ID " \
            "-authenticationKeyPath #{auth_key_path}",
  )
  upload_to_testflight(api_key: api_key, skip_waiting_for_build_processing: true)
end
```

Full commented template with every lane: `Fastfile.example` (same directory).
