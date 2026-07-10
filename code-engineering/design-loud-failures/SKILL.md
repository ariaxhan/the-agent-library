---
name: design-loud-failures
description: >-
  Design systems so a failure can never present as success. Use when building or
  reviewing pipelines, extractors, reconciliations, checkers, or any computation whose
  output humans act on; when missing inputs, unreadable files, or crashes could pass
  silently; when a tool "found" an explanation that feels too convenient; or on "make
  this fail loudly", "could this lie to us", "harden the failure paths". Produces named
  invariants, explicit skip and no-answer states, honest cause classes, and adversarial
  regression fixtures.
---

# Design Loud Failures

The dangerous state is not "the system failed." It is "the system failed and said
everything was fine." A wrong answer delivered with confidence costs more than no answer,
because humans act on it and stop checking. Every step below removes one way a system can
lie.

## 1. Name your invariants; do not search for coincidences

Verify the identities the domain guarantees ("these two totals must match", "parts must
sum to the whole") instead of searching combinations of values for something that agrees
within a tolerance. An unconstrained search over enough combinations will eventually
manufacture a plausible explanation for a real defect, and the defect ships wearing an
excuse. If you cannot name the invariant, you do not have a check; you have a slot machine.

## 2. Make "not provided" a first-class state

When an optional input is absent, the result is a named skip state: "not provided". Never
a fake pass (the check did not run), and never a leaked failure marker such as a sentinel,
placeholder, or error string flowing onward as data. Skips are reported alongside passes
and failures so a reader can see what was not checked.

## 3. Report the real cause class for unreadable inputs

When an input cannot be processed, distinguish the causes: extraction returned nothing,
the layout or format changed, the process crashed. Reporting the wrong cause ("file was
empty" when the parser crashed) sends humans to fix the wrong thing, and a tool that
misdiagnoses trains its users to ignore it. The diagnosis is part of the output contract.

## 4. Wrap every computation boundary

Any step that computes an answer gets a boundary wrapper: on crash, it degrades to an
explicit loud result meaning "no answer, zero fabricated output, human review required".
Downstream code must be unable to mistake that result for data. Partial output from a
crashed step is fabricated output.

## 5. Lock each behavior behind an adversarial fixture

The moment a new way to lie is discovered, add a regression fixture that actively tries
to make the system lie: the absent input, the crashing document, the coincidence-shaped
defect. The fixture asserts the loud behavior (correct skip state, correct cause class,
explicit no-answer), not merely the absence of an exception. Untested honesty regresses
silently, which is the exact failure mode this skill exists to prevent.

## 6. Re-run gates before declaring done

A worker's "it passed" is a claim, not proof. The integrator re-runs the gates
independently in their own context before declaring the work done. Self-reported green is
where silent failures re-enter the system after you engineered them out of it.

## When to fire

- A check, reconciliation, or validation is being designed or reviewed.
- An optional input can be absent and the code has an opinion about what that means.
- A parser, extractor, or external tool can fail on real-world input.
- A result "explains" a discrepancy and nobody can name the invariant behind it.
- A subordinate agent or teammate reports pass/fail you are about to relay.

## Not this skill

- Retry logic, backoff, or transient-error recovery.
- Alerting and monitoring infrastructure; this is about what the system reports, not how
  the report is delivered.
- Exception-handling style debates (checked vs unchecked, error codes vs exceptions).
  Any style works if failure states stay loud, named, and impossible to read as success.
