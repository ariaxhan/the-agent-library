---
name: review-ai-code-quality
description: Review AI-generated or recently changed code for common quality failures. Use when reviewing code, validating an implementation, checking "is this ready", auditing AI-authored changes, or looking for edge cases, validation gaps, error handling problems, duplication, and needless complexity. Produces prioritized findings and required fixes.
---

# Review AI Code Quality

AI-authored code often looks plausible while missing boring safeguards. Review the boring safeguards first.

## 1. Identify the changed surface

Inspect the diff or target files. Determine:

- Inputs and trust boundaries
- External calls
- State mutations
- Error paths
- User-visible behavior
- Tests or checks that cover the change

## 2. Run the Big Five review

### Input validation

Every external input should be parsed or validated at the boundary. Look for raw request bodies, unchecked params, untyped JSON, unsafe casts, and string-built queries.

### Edge cases

Check null, empty arrays, empty strings, zero values, unicode, timeouts, large inputs, duplicate inputs, and missing optional fields.

### Error handling

No empty catches. No swallowed errors on important paths. User-facing messages should be safe and logs should include context.

### Duplication

Repeated logic in three or more places should usually become one helper. Two copies may be fine; do not abstract too early.

### Complexity

Flag deeply nested conditionals, large functions, multi-purpose modules, and clever code with unclear invariants.

## 3. Check tests

Ask:

- Is the main success path covered?
- Are failure paths covered?
- Are edge cases covered?
- Do assertions check meaningful behavior?
- Would the test fail if the implementation were wrong?

High coverage with weak assertions is not quality.

## 4. Produce findings

For each finding:

- Severity
- File/location
- Problem
- Why it matters
- Concrete fix
- Suggested test, if relevant

Lead with blockers. Keep nits separate.

## 5. Verdict

End with:

- Ready / needs fixes / unsafe to ship
- Required fixes before merge
- Optional improvements
- Checks you could not run
