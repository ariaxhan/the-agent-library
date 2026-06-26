---
name: critique-vision-handoff
description: Adversarially review vision handoff docs, seed docs, architecture briefs, or implementation plans before they reach coding agents. Use when the user asks to "critique this vision", "review my handoff", "stress test this spec", "break this plan", "find the holes", or check whether a planning document is ready for implementation. Produces a severity-rated critique with concrete fixes.
---

# Critique Vision Handoff

Find the gaps that would make a coding agent waste time, guess wrong, or build the wrong thing.

Be direct and constructive. Every issue needs a consequence and a fix. Critique the what and why, not implementation choices the coding agent should own.

## 1. Establish the stakes

Identify the context:

- Hackathon/prototype
- Production system
- Library/API
- Internal tool
- Research experiment

If stakes are unclear, state the assumed stakes and calibrate severity around them.

## 2. Run the six critique layers

### Structural integrity

Ask whether the document stands alone, stays internally consistent, includes required sections, and speaks to the intended audience.

### Decision archaeology

Check whether decisions are specific, rationales are present, rejected alternatives are documented, and constraints have sources.

### Complexity audit

Look for feature creep, excess components, unnecessary abstractions, and fragile dependency load.

### Ambiguity detection

Flag weasel words, missing edge cases, implicit assumptions, and vague success criteria.

### Risk surface

Check external failures, scale assumptions, security exposure, migration path, and operational failure modes.

### Implementation readiness

Verify the first step, priorities, definition of done, and permission for the coding agent to push back.

## 3. Apply critique techniques

Use at least three:

- Naive Robot Test: read literally with zero context.
- Adversarial User Test: misuse or overload the system.
- Time Travel Test: debug it six months later.
- Subtraction Test: remove features and see what still works.
- Why Ladder: ask why three times for each major decision.
- Contradiction Hunt: compare sections for drift.

## 4. Write the critique

Use severity buckets:

- `BLOCKER`: cannot proceed until fixed
- `MAJOR`: will cause implementation pain or wrong work
- `MINOR`: polish or clarity issue
- `NITPICK`: optional style issue

For each finding:

- Location
- Problem
- Why it matters
- Fix

Also include:

- What is good
- Simplification opportunities
- Questions the coding agent will ask
- Recommended next steps

## 5. Avoid bad critique

Do not:

- Nitpick formatting unless it harms understanding
- Fight explicitly documented technology decisions
- Add process that does not improve implementation
- Convert taste preferences into blockers

Before finalizing, ask: if the author fixes everything here, is the document actually better?

Use `reference/techniques-and-output.md` for the full output template and anti-pattern list.
