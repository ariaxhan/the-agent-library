---
name: write-session-chronicle
description: Write an honest session chronicle after substantial work. Use when wrapping up coding, research, writing, planning, or agent work; when the user asks to "write the chronicle", "record what happened", "wrap this up", "leave a handoff", or preserve decisions/failures for the next session. Produces a chronicle document with changed files, checks, failures, deferred work, and disagreements.
---

# Write Session Chronicle

A chronicle is the honest account of what happened. It is not a victory lap. It should help a future agent resume work without trusting stale claims.

## 1. Locate the record

Use the project's existing convention if present. Otherwise create:

```text
_meta/chronicles/YYYY/YYYY-MM-DD-short-slug.md
```

If no `_meta/` exists, use:

```text
docs/chronicles/YYYY-MM-DD-short-slug.md
```

If the work had a commission, link it.

## 2. Reconstruct reality

Inspect:

- Git status and diff
- Commands/tests/checks run
- Files created, edited, moved, or deleted
- User corrections and changes in direction
- Known failures or skipped checks
- Open questions and deferred tasks

Do not rely on memory when the filesystem can answer.

## 3. Write the chronicle

Include:

- Metadata: date, status, related commission or task
- Trigger: what started the work
- Attempted: what the session tried to do
- Changed: concrete file/path changes
- Checked: commands or review steps that actually ran
- Failed: wrong turns, false premises, broken checks
- Deferred: exact remaining work and where it is tracked
- Disagreements: where the agent or user corrected direction
- Current truth: what future work should believe

## 4. Be specific

Good:

- "Renamed `skills/foo` to `skills/bar` and updated frontmatter."
- "`python3 -m json.tool` passed on plugin metadata."
- "Full validator did not run because PyYAML was unavailable."

Bad:

- "Cleaned things up."
- "Everything works."
- "Some tests were run."

## 5. Preserve course corrections

If the session changed direction, record the before/after. A wrong turn that got corrected is valuable context.

## 6. Finish with next moves

End with the highest-signal next actions:

- What to do next
- What not to repeat
- Which files are the source of truth
- Which checks need to be rerun later
