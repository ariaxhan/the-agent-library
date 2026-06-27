---
name: secure-keys
description: Audit and lock down how AI tools hold API keys and credentials. Finds exposed keys across code, config files, .env files, environment variables, shell history, and git history; moves connections to OAuth / "Sign in with X" where one exists; migrates the rest into secure storage (macOS Keychain, a cloud secrets manager, or Cloudflare AI Gateway) with runtime retrieval instead of files; flags what to rotate; and tightens scope, spend caps, expiry, and IP rules. Trigger on "secure my keys", "audit my credentials/secrets", "find exposed API keys", "lock down my secrets", "key hygiene", "did I leak a key", or after wiring up an MCP server or a new integration.
---

# Secure Keys

Audit and harden how the user's AI tools authenticate with external services. Run the phases in order. Read first; change only after showing a plan and getting a yes.

## Absolute rules — never violate

- **Never print, echo, log, or display a secret value.** Refer to a key only by name and location, e.g. `OPENAI_API_KEY in .env:3`. When showing matches, redact the value to a prefix like `sk-…`.
- **Never ask the user to paste a key into the conversation.** If a value must be entered, give them a command to run that reads it off-screen (their shell, a tool prompt), and have the tool store it directly.
- **Destructive steps require explicit confirmation first** — rotating, revoking, deleting a key, or rewriting git history. State the blast radius before doing any of them.
- **Discovery is read-only.** Migrate one credential at a time and verify it live before moving on. Never batch-and-pray.

## Phase 1 — Discover (read-only)

Find credentials and report **location + type only, never the value**:
- Files: `.env*`, and config like `.mcp.json`, `**/claude_desktop_config.json`, `.cursor/`, `.vscode/`, plus `*.json|*.yaml|*.toml` holding key-shaped values.
- Source: grep for key shapes — `sk-`, `sk-ant-`, `AIza`, `ghp_`/`gho_`, `xox`, AWS `AKIA`, generic `Bearer ` tokens.
- History: `~/.zsh_history` and `~/.bash_history`, current env vars, and `git log -p` / `git grep` across history for committed or pushed secrets.

Output a table: **name · location · type** (LLM key / connected-account token / cloud cred / signing key) · **exposed?** (committed, pushed, or in shell history = yes).

## Phase 2 — Classify

Split findings into:
- **(a) Could use a login instead** — a "Sign in with Google/GitHub/…" OAuth flow or a managed connector exists. List the migration path for each. Prefer this; a revocable, scoped login beats a long-lived key.
- **(b) Must stay a key** — model API keys, signing keys, tokens with no OAuth path. These go to secure storage in Phase 4.

## Phase 3 — Triage exposure

Anything in committed files, pushed history, or shell history is compromised. Mark it **rotate**, top priority. Order by blast radius: account-access tokens (email, drive, repo, cloud) before spend-only model keys, because money is cappable and access is not.

## Phase 4 — Recommend storage (name the tradeoff)

For each must-keep key, recommend a home and say plainly **who ends up holding it**:
- **macOS Keychain** (`security`): local, free, does not sync. Best default for single-machine dev keys.
- **Cloud secrets manager** (1Password `op run`, Bitwarden, AWS Parameter Store, GCP Secret Manager, Doppler, Infisical): syncs across devices, survives a dead laptop, trusts a vendor; the key still reaches the machine at use.
- **Cloudflare AI Gateway (BYOK)** — LLM provider keys only: the real key never touches the machine, the user carries a gateway token instead. Free.

Recommend by the user's actual setup. Ask which they want; never assume.

## Phase 5 — Migrate (one at a time, verified)

Store the key in the chosen vault, then rewrite each app, script, or MCP server to **fetch it at runtime** (`security find-generic-password`, `op run --`, or the gateway endpoint) so config holds only a pointer. Run the tool once to confirm it still works.

## Phase 6 — Harden

For each key, apply the smallest practical scope, a spend cap, an expiry, and an IP allowlist where the provider supports them. Then walk the user through revoking and reissuing every **rotate** key from Phase 3.

## Phase 7 — Verify

Re-run Phase 1 and confirm zero plaintext keys remain in code, configs, `.env`, env vars, and shell history. Report what changed, what was rotated, and anything still exposed and why — without ever showing a value.
