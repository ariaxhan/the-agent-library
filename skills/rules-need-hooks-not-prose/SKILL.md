---
name: rules-need-hooks-not-prose
description: Enforce the agent rules that must never break with hooks the agent can't bypass — secret scans, destructive-command guards, format gates — instead of prose instructions it quietly ignores under load.
---

# Rules Need Hooks, Not Prose

## The finding

A rule written as a sentence in a config file gets violated roughly **40% of the time
under pressure**. The same rule encoded as an enforcing hook approaches **zero**. Long
context, a hard task, and time pressure are exactly when a model stops re-reading its
instructions — which is exactly when the rules matter most. Aspiration is not enforcement.

So the test for any must-hold behavior is blunt: **if it truly cannot be allowed to break,
it has to be a hook, not a paragraph.** If it's only a paragraph, assume it will break.

## Skeleton vs judgment — the split is the deliverable

Not every rule can or should be a hook. The valuable move is honestly sorting them:

- **Skeleton** — mechanically checkable, binary pass/fail, no taste required. These get
  hooks. Examples: a hardcoded secret, a destructive command on something you didn't
  create, a push to the protected branch, a file exceeding a line budget, a missing
  required field/format.
- **Judgment** — requires taste or context, can't be reduced to a regex. These stay
  methodology — routed to skills, docs, and review. Examples: "make the smallest viable
  change," "verify it live," "is this abstraction worth it," "is the premise even right."

Trying to hook a judgment rule produces brittle false-positives; trying to prose-enforce a
skeleton rule produces silent violations. Doing the split cleanly is the actual work.

## What to hook (concrete)

- **Secret detection** — block any commit/write containing a key-shaped or token-shaped
  string. Catches the credential leak before it leaves the machine.
- **Destructive-command guard** — intercept `rm -rf`, `git reset --hard`, `clean -fdx`,
  `branch -D`, force-push on paths the session didn't author; require confirmation first.
- **Push-to-protected-branch confirmation** — refuse a direct push to `main`/`master`
  unless explicitly allowed for this repo.
- **Budget / size caps** — reject a file or diff over a set line count without an override.
- **Format / structure gates** — require the commit message shape, the required frontmatter
  field, the passing linter, before the action completes.

## What to leave as methodology

Smallest-change discipline, verify-live, premise-auditing, "boring beats clever,"
investigate-before-mutating. These need a thinking agent, not a regex. Put them in a skill
or a reference the agent loads at the relevant moment — and accept they'll be followed by
disposition, not guaranteed by a gate.

## Hook types & where they fire

- **PreToolUse guard** — fires *before* a tool runs; can block it. The right place for
  destructive-command and protected-branch guards (stop the action, don't clean up after).
- **Pre-commit scan** — fires on commit; the right place for secret detection and format
  gates. Bytes never reach history if it fails.
- **Stop / completion gate** — fires when the agent tries to finish; the right place to
  force a required artifact (a record, a passing-test check) before "done" is allowed.

## The override escape-hatch

Real exceptions exist, so build one deliberate, visible door — never an off-switch. Pattern:
the hook passes if (and only if) an explicit override token appears in the commit message or
action, *with a reason*:

```
[budget-override: vendored lib, generated file] feat: import upstream parser
```

The token forces the human-or-agent to name *why* the rule is being suspended, leaves an
audit trail in history, and keeps the bypass rare and intentional. A rule with no escape
hatch gets disabled wholesale the first time it's wrong; a rule with a *logged* hatch stays
on.
