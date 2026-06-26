---
name: refactor-code-safely
description: Refactor code without changing behavior. Use when the user asks to clean up, simplify, rename, restructure, extract, inline, move code, reduce duplication, or modernize internals while preserving behavior. Produces a scoped refactor with before/after checks.
---

# Refactor Code Safely

Refactoring changes structure, not behavior. If behavior changes, it is a feature or bug fix, not a refactor.

## 1. Establish baseline

Run the nearest relevant tests or checks before editing. If no tests exist, identify how current behavior will be preserved.

For risky code, create temporary characterization tests: tests that capture what the code does now.

## 2. Audit scope

Find every instance of the symbol, pattern, module, route, or component involved. List the intended scope before editing.

If the change touches many files, split it into smaller transformations.

## 3. Define the exact transformation

Choose one:

- Rename
- Extract function/module
- Inline wrapper
- Move code
- Remove dead code
- Simplify conditional
- Deduplicate repeated logic

Do not mix unrelated transformations.

## 4. Execute one transformation

Keep edits mechanical and boring. Avoid opportunistic improvements.

Rules:

- Extract only when at least three real uses justify it, unless the current function is already unsafe to work in.
- Inline wrappers with one call site.
- Remove dead code only after confirming it is unused.
- Update tests/docs only where required by the same transformation.

## 5. Verify behavior

Run the baseline checks again. For behavior-sensitive code, compare old and new outputs on the original input set.

If checks fail, stop and fix or revert the last transformation before continuing.

## 6. Report

Return:

- Transformation type
- Scope searched
- Files changed
- Checks before and after
- Any behavior risk
- Any follow-up that should be a separate task
