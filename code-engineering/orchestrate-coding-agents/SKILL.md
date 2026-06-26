---
name: orchestrate-coding-agents
description: Coordinate multiple AI coding agents safely. Use when splitting implementation, review, testing, research, or refactor work across agents; when tasks can run in parallel; or when the user asks to orchestrate, spawn agents, delegate, parallelize, or manage tiered work. Produces scoped contracts, isolated work, and merged findings.
---

# Orchestrate Coding Agents

Orchestration is coordination, not implementation. Define contracts, isolate work, verify outputs, then merge deliberately.

## 1. Decide whether to split

Parallelize only when work can be separated by file, concern, or artifact.

Good splits:

- Security review and performance review
- Independent modules
- Research versus implementation
- Test writing versus docs

Bad splits:

- Multiple agents editing the same files
- Vague "improve everything"
- Tasks with hidden shared state

## 2. Write contracts

Each agent gets:

- Goal
- Allowed files or artifacts
- Allowed tools
- Forbidden actions
- Expected output path
- Verification command or review criteria
- Return format

The contract must be rejectable. If the goal or scope cannot be checked, it is not ready to delegate.

## 3. Isolate work

Use separate worktrees, branches, folders, or output files when possible. No two concurrent agents should edit the same file unless the merge protocol is explicit.

If isolation is unavailable, serialize edits and parallelize only read-only review.

## 4. Require durable output

Agents should write findings or artifacts to files, not only chat summaries. A summary is intent; the file/diff is evidence.

Before accepting work:

- Open the changed files or report.
- Check scope boundaries.
- Run relevant commands.
- Compare result to the contract.

## 5. Merge and synthesize

For multiple reports:

- Deduplicate findings
- Rank by severity
- Resolve contradictions
- Identify blockers
- Turn vague feedback into concrete tasks

For code branches:

- Review diff
- Verify allowed files only
- Run checks
- Merge one logical change at a time

## 6. Escalate

Stop and ask for direction if:

- Contracts overlap unexpectedly
- Agents disagree on a blocker
- Sensitive scopes are touched
- Verification cannot run
- Output exceeds the agreed scope
- Work needs destructive or irreversible operations

## 7. Final report

Return:

- Agents/tasks spawned
- Contracts
- Files or reports produced
- Checks run
- Accepted/rejected outputs
- Remaining blockers
