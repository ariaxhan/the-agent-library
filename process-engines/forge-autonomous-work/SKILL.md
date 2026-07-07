---
name: forge-autonomous-work
description: Run a bounded autonomous work loop that generates competing approaches, implements iteratively, runs acceptance checks, stress-tests the result, learns from the output, and either ships or reports why it cannot. Use when the user asks to "forge this", "run autonomously", "take this end to end", "iterate until done", "iterate until tests pass", or provides runnable acceptance criteria for hands-off implementation. Produces an artifact, evidence log, passing checks or escalation record, and final verdict.
---

# Forge Autonomous Work

Forge is a process engine for substantial work. It does not take the first plausible plan. It heats alternatives, hammers one into shape, quenches it under pressure, tempers it by measuring what happened, and anneals if the structure is brittle.

Use this for complex coding, research, writing, planning, or operational tasks where success can be checked.

## 0. Preflight

Before starting, define:

- Goal
- Scope
- Hard boundaries
- Budget or iteration cap
- Verification method
- Stop conditions
- Acceptance commands, if this is an implementation task

If there is no checkable end state, do not forge. Use a planning or dream skill first.

When the user provides a SPEC/GOAL/ACCEPTANCE block, run Forge in acceptance mode:

```text
SPEC: short name
GOAL: observable outcome
ACCEPTANCE:
  - runnable command or check
FILES: optional scope
MAX_ITERATIONS: optional, default 5
```

Stop and clarify if every acceptance criterion is manual or opinion-based, the goal is vague, or the allowed file scope is risky.

## 1. Heat: generate competing approaches

Create 2-3 meaningfully different approaches. For each:

- Strategy
- Files/artifacts affected
- Expected benefit
- Known risks
- Verification method
- Testable hypothesis

Avoid fake variety. "Same plan with different wording" does not count.

For small tasks, one approach is fine if the solution is obvious and low-risk.

## 2. Hammer: iterate against checks

Pick the strongest approach and work in tight loops:

1. Create or identify the failing/unfinished check.
2. Make the smallest change that could pass.
3. Run the check.
4. Fix implementation, not the check, unless the check is wrong.
5. Record what changed.

For acceptance mode, create an iteration log at `_meta/autonomous/YYYY-MM-DD-short-slug.md` or `docs/autonomous/YYYY-MM-DD-short-slug.md` when no `_meta/` exists. Record the goal, acceptance commands, scope, iteration count, files changed, check outputs, and escalation reason if any.

If the same failure survives three attempts, classify it:

- **Approach gap:** the strategy is wrong; try another approach.
- **Contract gap:** the goal is ambiguous or impossible to verify; stop and report the gap.

Do not burn cycles on a contract gap.

Escalate instead of looping forever when any guardrail trips:

- max iterations reached
- same error signature appears 3 times
- 3 iterations make no acceptance progress
- required dependency or credential is missing
- scope needs to expand materially
- a destructive or irreversible operation would be needed
- checks are flaky or not measuring the goal

## 3. Quench: stress-test the result

Attack the output:

- What input breaks it?
- What edge case was missed?
- What assumption is false?
- What fails at larger scale?
- What does a skeptical user dislike?
- What changed outside scope?
- What evidence is missing?

Write concrete failing checks or examples when possible.

Score:

- `survived`: no major issues
- `cracked`: fixable issues
- `shattered`: approach is structurally wrong

Cracked goes back to hammer. Shattered goes to anneal.

## 4. Temper: learn from the output

Measure what happened:

- Did the hypothesis hold?
- What surprised you?
- What took longer than expected?
- What checks caught real issues?
- What pattern should future work reuse or avoid?

If temper finds a missed issue, return to hammer. If it finds a useful lesson, record it in the final report.

## 5. Anneal: change structure

If an approach shattered:

1. Record why.
2. Mark that class of approach as failed.
3. Return to heat with the failure as a constraint.
4. Choose a structurally different approach.

Stop after three shattered approaches or the iteration cap.

## 6. Final verdict

Return:

- What shipped or was produced
- Approaches considered
- Checks run
- Iterations used and iteration log path, if acceptance mode ran
- Stress-test findings
- Lessons learned
- Remaining risks
- Why it stopped, if unfinished

Never report success without evidence.
