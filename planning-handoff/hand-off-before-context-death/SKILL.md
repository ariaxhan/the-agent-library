---
name: hand-off-before-context-death
description: >-
  Write the session handoff while the verified context is still loaded, before the
  window or budget runs out. Use when context is running low mid-work, when pausing
  substantial work ("wrap up", "hand this off", "save state for the next session",
  "we'll pick this up later"), or when a session is stuck re-reading the same failure.
  Ten minutes of writing while context is loaded replaces hours of rediscovery.
---

# Hand Off Before Context Death

A working session ends one of two ways: with its knowledge written down, or with its
knowledge gone. The state you hold near the end of a session (what is verified, what is
actually broken, what the real next move is) took the whole session to build, and it decays
to zero the moment the session ends. Writing the handoff **while that context is still
loaded** costs minutes. Writing it after, from a cold start, re-pays the entire exploration.
Observed across production agent runs, the sessions that skipped this step forced their
successors to rediscover the same dead ends before doing any new work.

## The priority rule

When context or budget is constrained, **inheritance outranks remaining implementation.**
Unfinished code is cheap: a later session writes it in an hour from a good handoff. Lost
context is not recoverable at any price. The moment you notice the window closing, stop
building and start writing, even mid-feature.

## Stop conditions (when to write it)

- **The gate is green, the evidence is recorded, the work is pushed: stop improving.**
  Polish without a named defect is scope creep in a work shirt; write the handoff instead.
- **You have re-read the same failing output three times without a new hypothesis: stop.**
  You are looping, and self-detection of looping is unreliable. Write the handoff and hand
  the failure to a fresh context; a cold reader with your notes beats a hot reader with
  your fatigue.
- **Context is measurably low and substantial work remains: stop building now**, while you
  can still write an accurate map.

## What the handoff contains

- **A state map with evidence.** For each piece touched: its state and the named proof
  (the command run, the count seen, the commit). "Auth works" is a claim; "auth suite, 34
  tests green on <sha>" is inheritance.
- **The true next action, re-pointed.** Not the plan from the start of the session; the one
  thing the next session should actually do first, given everything learned since. Stale
  next-actions send successors down roads you already closed.
- **Failures and disagreements, preserved.** What was tried and did not work, and why. What
  you disagreed with and did anyway (or refused). Deleting the failures forces the next
  session to buy them again at full price.
- **Reality hooks.** Checkable claims a later session can re-test cheaply: "the flaky test
  is X, reproduce with Y", "the response should contain Z". These let the successor verify
  the handoff instead of trusting it.

## Anti-patterns

- **"Just one more fix" past the closing window.** You get neither the fix nor the handoff.
- **A handoff that is a plan, not a map.** Aspirations without state and evidence tell the
  next session nothing about what is real.
- **Smoothing over the failures.** A handoff that reads like a success story hides exactly
  the information that was most expensive to learn.
- **Writing it from memory the next day.** The whole value is the loaded context; after it
  unloads, you are a stranger summarizing hearsay.
- **Grinding a failure past the third re-read.** More staring is not a hypothesis; a fresh
  context with your notes is.

## Output

One handoff document containing: the state map with named evidence per piece, the single
re-pointed next action, the preserved failures and disagreements, and the reality hooks.
Committed or saved where the next session will look first.
