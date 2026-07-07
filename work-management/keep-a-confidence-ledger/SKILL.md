---
name: keep-a-confidence-ledger
description: >-
  Maintain one honest map of what is actually true about every subsystem in a project.
  Use when landing or verifying work changes a subsystem's state, at session close, or
  when someone asks "what's the state of X", "is X done", "how far along are we",
  "what's actually working". Replaces percentages and vibes with exactly four evidence-
  backed states, so a handoff or a status answer never overstates reality.
---

# Keep a Confidence Ledger

Every project accumulates claims about its own state: "auth is done", "search mostly works",
"deploy is 90% there". Most of those claims were true once, for some definition of done,
according to the person who wrote the code. A confidence ledger is the single file that
answers, for every subsystem, the only question that matters at handoff: **what is actually
true, and how do we know?** A wrong row is worse than a missing feature, because people build
on it.

## The four states (exactly one per row, no percentages)

- **complete**: verification evidence exists and is NAMED in the row: the command, the CI
  run, the test count, the date. "Complete" without evidence is a lie with good posture.
- **needs-polish**: works, with a KNOWN, WRITTEN gap ("no date filter; sorting is
  insertion order"). The gap text is the point; "needs polish" alone is banned.
- **blocked**: waiting on something external, with the EXACT unblock step ("client shares
  API keys, then set the secret and run the live smoke test"). A block without an unblock
  step is a complaint, not a state.
- **future-phase**: deliberately not built; points at a dated decision or a scope document
  that says so.

No fifth state, no "almost", no "80%". A percentage is a feeling wearing a number; none of
the decisions a reader makes (trust it, fix it, chase the blocker, ignore it) map to one.

## Flip rules

- **States are set by verification evidence, never by the author of the change.** Whoever
  wrote the code proposes; the evidence decides. Observed across production agent runs,
  author-flipped rows are the single largest source of false "complete".
- **Evidence must be re-runnable**: a command plus expected result, or a CI/commit link.
  Prefer "12 files, 111 tests green on <sha>" over "tests pass".
- **Downgrades are the ledger working.** Discovering a row was optimistic and correcting
  it is the mechanism doing its job. Silent optimism is the failure mode, not the downgrade.
- **Update in the same session as the state change**, while the evidence is fresh. A ledger
  updated "at some future cleanup" is a fiction with a file name.

## Reading the ledger (for a fresh session or reviewer)

Trust rows whose evidence you could re-run. Re-verify rows whose evidence predates newer
commits touching that subsystem: check the log for the row's paths, and if commits are newer
than the row's date, re-run its stated command before trusting it. The blocked rows,
collected, are the project's external dependency list; read them before promising anything
live.

## Anti-patterns

- **Percentages or "almost done".** They encode confidence, not state, and nobody can act
  on them.
- **The author flipping their own row to complete.** The claim and the proof come from the
  same source; that is not verification.
- **Evidence by adjective.** "Thoroughly tested" is not evidence; a named command with an
  expected count is.
- **Treating a downgrade as failure.** Punishing honest corrections trains the ledger to lie.
- **Trusting an old row after new commits.** Evidence has a date; code moved after that date
  makes the row a hypothesis again.

## Output

Maintain one ledger file with a row per subsystem:

- Subsystem | state (one of the four) | evidence or gap or unblock step or decision pointer | date.
- On every state change: the updated row, in the same session as the change.
- At read time: which rows were trusted as-is, which were re-verified, and what the re-run showed.
