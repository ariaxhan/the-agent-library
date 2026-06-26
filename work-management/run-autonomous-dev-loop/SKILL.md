---
name: run-autonomous-dev-loop
description: Run a bounded autonomous implementation loop against runnable acceptance criteria. Use when the user provides a SPEC/GOAL/ACCEPTANCE block, asks to "run autonomously", "iterate until tests pass", "self-correct this build", or wants hands-off implementation with explicit guardrails. Produces code changes plus an iteration log, passing checks or an escalation record.
---

# Run Autonomous Dev Loop

Implement, validate, fix, and stop when acceptance passes or the loop hits a guardrail. This skill only works when success can be checked by commands.

## 1. Validate the spec

Require:

```text
SPEC: short name
GOAL: observable outcome
ACCEPTANCE:
  - runnable command or check
FILES: optional scope
MAX_ITERATIONS: optional, default 5
```

Stop and ask for clarification if:

- There is no acceptance criterion.
- All criteria are manual/opinion-based.
- The goal is vague.
- The allowed file scope is risky or unclear.

## 2. Create an iteration log

Default path:

```text
_meta/autonomous/YYYY-MM-DD-short-slug.md
```

If no `_meta/` exists, use:

```text
docs/autonomous/YYYY-MM-DD-short-slug.md
```

Record:

- Goal
- Acceptance commands
- Scope
- Max iterations
- Current iteration
- Changes made
- Check outputs
- Escalation reason, if any

## 3. Implement the smallest viable change

For each iteration:

1. Inspect existing code and tests.
2. Make the smallest change that could satisfy acceptance.
3. Avoid unrelated refactors.
4. Record files changed in the iteration log.

If the change expands beyond the declared scope, stop and ask.

## 4. Run acceptance checks

Run every acceptance command. Capture:

- Command
- Exit code
- Relevant output
- Whether it improved from the previous iteration

Do not skip a check because another one passed.

## 5. Evaluate

If all checks pass, stop and report success.

If checks fail, create a fix note:

- Failed command
- Error signature
- Likely cause
- What was tried
- What not to repeat
- Next change

Then start the next iteration.

## 6. Escalate instead of looping forever

Stop and escalate if any guardrail trips:

- Max iterations reached
- Same error signature appears 3 times
- 3 iterations make no acceptance progress
- Required dependency/credential is missing
- Scope needs to expand materially
- A destructive or irreversible operation would be needed
- The checks are flaky or not actually measuring the goal

## 7. Final report

Return:

- Outcome: passed or escalated
- Iterations used
- Files changed
- Checks run
- Remaining failures, if any
- Iteration log path

Never claim success without passing the declared acceptance checks.
