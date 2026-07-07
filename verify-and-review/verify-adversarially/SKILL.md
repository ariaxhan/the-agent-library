---
name: verify-adversarially
description: >-
  Earn "done" by splitting verification into two roles: a fresh-context agent attacks
  the work, and the coordinator adjudicates every finding. Use before declaring a
  subsystem complete, before trusting a green report, after delegated work returns, or
  on "verify this", "is it actually done", "attack this change", "red-team this",
  "prove it works". Green tests prove the code does what the tests say; this pass
  proves the tests say enough.
---

# Verify Adversarially

The author of a change is the worst person to verify it: they test what they expect, and
their expectations are exactly what shaped the bug. Adversarial verification separates the
two jobs. One party attacks with no knowledge of how the thing was built; another judges
what the attack found. Observed across production agent runs, this split routinely surfaces
defects that green suites and confident self-reports had already blessed.

## The split (never collapse it)

- **A fresh-context agent attacks.** It receives the attack-surface list and the artifact
  or repo path, NOT the implementation narrative, NOT the author's confidence, NOT the list
  of things already checked. Contaminated context finds what you expect; fresh context finds
  what you missed.
- **The coordinator adjudicates.** Every finding gets one of three verdicts, each with a
  written reason: **real** (fix now), **real-but-later** (record where future work is
  tracked, explicitly, not into the void), **false positive** (say why). Attackers never
  decide severity, and the author of a change never grades their own work.

## Build the attack-surface list

Before the pass, write down where the change can hurt: boundary inputs, concurrent or
repeated calls, permission and isolation seams, injection through stored content, error
paths that can masquerade as success, claims the artifact makes that a reader would rely on.
Reuse the list across passes and extend it per change; the list is an asset, the pass is an
event.

## Adjudication rules

- **Reproduce before fixing.** A finding without a failing command, test, or observable
  behavior is a hypothesis, not a defect. Get the reproduction first.
- **Every real finding lands as a regression test in the same commit as its fix.** A fix
  without its test is a defect on a timer.
- **Zero findings is itself suspicious.** Before celebrating, check the attacker actually
  exercised the surface: its transcript should name concrete inputs it tried. An attacker
  that only read the code and agreed with it did not attack.

## Read evidence, not verdicts

An attacker's PASS or FAIL label is a claim like any other. Read the underlying evidence:
the command output, the response body, the rendered result. A FAIL can be an overstated
self-report; a PASS can hide an out-of-scope miss. And check artifact freshness before
believing any gate: a green report can be a stale report left over from a previous run.
Compare the report's timestamp against the code it claims to cover, and prefer gates that
fail loudly when their output is stale.

## Anti-patterns

- **Briefing the attacker with the implementation story.** You have just installed your own
  blind spots in the reviewer.
- **Letting the attacker set severity.** Attack and judgment are different jobs; collapsing
  them replaces adjudication with whoever wrote the most alarming sentence.
- **Fixing findings nobody reproduced.** You may be "fixing" a false positive and breaking
  something real.
- **Celebrating a clean pass without checking coverage of the surface.** Silence is only
  meaningful if the attack happened.
- **Trusting a green report without checking it is fresh.** Stale artifacts pass forever.

## Output

Return:

- The attack-surface list used, with any per-change extensions.
- Every finding with its verdict (real / real-but-later / false positive) and the reason.
- For each real finding: the reproduction, the fix, and the regression test that landed with it.
- Where each deferred finding is now recorded.
- For a zero-finding pass: the evidence the attacker exercised the surface.
