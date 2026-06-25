---
name: verify-live-not-committed
description: Make an AI agent prove a change works against the live, running system before calling it done — running it, curling the served asset, watching the test pass — instead of inferring success from a commit.
---

# Verify Live, Not Committed

## The rule

"Done" means **verified against the live, running system** — you ran it, curled it, saw
the test pass, exercised the actual code path. It never means "I committed the change."
Before reporting any user-facing change as done, run one command that confirms real
runtime state. If you didn't run such a command, the change is not done.

## Why it matters

This is the single largest source of wasted back-and-forth rounds in agent work. The gap
between "I wrote the code" and "the code works" is exactly where regressions, typos, bad
config, and unmade assumptions hide. A commit is a record of intent, not evidence of
behavior. Code that reads correctly silently betrays you on real data all the time — the
only thing that catches it is exercising it.

## The chain — every link can break

```
committed  ≠  pushed  ≠  deployed  ≠  working
```

- **Committed** — the diff exists locally. Proves nothing ran.
- **Pushed** — the remote has it. Still nothing ran.
- **Deployed** — the new bits are live. They may still error on the first request.
- **Working** — you observed the correct runtime behavior. This is the only "done."

Reporting "done" from any link left of the last one is a claim you have not verified.

## How to verify live, by change type

- **Web / frontend** — `curl` the served asset (or hit the URL) and confirm the new
  markup/bytes are actually being served. Don't trust the build log; fetch the thing.
- **API / backend** — hit the endpoint with a real request and assert the response
  (status + body), not just that the server booted.
- **Test / logic fix** — run the test and watch it pass. A test you didn't run is a
  test that might not even compile.
- **Deploy / infra** — run the deploy/health check and confirm the new revision is the
  one actually serving, not the previous one still live.
- **Data / migration** — query the post-state and confirm the rows/shape changed as
  intended, with the rollback path known.

## The honest fallback

Some changes genuinely can't be checked headlessly — an on-device flow, a manual UI
path, something behind a human gate. Do **not** fake verification you couldn't perform; a
claimed "verified" that was really inferred is worse than an honest hand-off. Instead,
name the residual and hand the check back:

> **"Deployed — your check."**  *(never "it works")*

State exactly what you did verify, and exactly what remains unobservable from where you
sit. Honesty about the boundary is part of the deliverable.

## The one-line gate

Before writing "done," ask: **"What command did I run that proves this live?"**
If there isn't one, the status is "deployed — your check" or "deferred" — not "done."
