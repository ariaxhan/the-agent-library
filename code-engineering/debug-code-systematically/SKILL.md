---
name: debug-code-systematically
description: Debug code with a scientific method instead of guessing. Use when fixing bugs, regressions, crashes, stack traces, failing tests, unexpected behavior, or "not working" reports. Produces a reproduced failure, tested hypotheses, isolated root cause, fix, and regression check.
---

# Debug Code Systematically

Debugging is theory work. Reproduce, hypothesize, isolate, fix root cause, and prove the original failure is gone.

## 1. Reproduce

Capture:

- Exact input or action
- Expected behavior
- Actual behavior
- Error output or stack trace
- Environment
- Frequency

If reproduction is not possible, add targeted logging or a minimal observation plan before changing code.

## 2. List hypotheses

Write at least three plausible causes before pursuing one. Read all error output first.

For each hypothesis, name what evidence would disprove it. Do not chase the first explanation that feels right.

## 3. Isolate

Use binary search:

- Call chain: inspect the midpoint, then recurse into the failing half
- Git history: bisect between known-good and known-bad
- Input: cut the failing input until the minimal case remains
- Boundaries: log inputs/outputs at module or service edges

Stop exploring when the failure is localized to a specific function, commit, input shape, or external dependency.

## 4. Find root cause

State the violated invariant in one sentence.

Do not patch only the visible failure site unless that is the actual defect. A null check at a crash site is usually not enough; ask why null arrived there.

## 5. Fix with a regression check

Make the smallest root-cause fix. Add or update a test/check that fails before the fix and passes after.

Run:

- The original failing case
- The regression check
- Nearby edge cases
- The nearest relevant test suite

## 6. Report evidence

Return:

- Reproduction
- Root cause
- Files changed
- Regression check
- Commands run and results
- Any residual risk

If you could not reproduce or fully verify, say that directly.
