---
name: debate-decisions
description: >-
  A compact decision protocol for non-trivial choices, reviews, governance calls, and
  live disagreement. Use when evidence alone cannot fully settle the decision. Skip for
  trivial, cheap-to-reverse, or deterministically decidable choices.
---

# Debate Protocols

Use debate as a small decision aid, not a format museum. If grep, tests, logs, source files, or official records can decide the question, use them as the judge and skip debate.

## Core Rules

1. State the resolution in one sentence.
2. Assign sides before arguing. For peer agents, the proposer argues against their own proposal and the reviewer argues for it; otherwise use a coin flip or a stable hash of the resolution.
3. Treat assigned side as a role, not belief. Concession is allowed and counts as progress.
4. The proposer must argue against their own proposal at least once.
5. End with a decision record: winner, strongest argument, unresolved risk, evidence that would flip the result, and preserved dissent.
6. Make every dissent testable. An objection must name the evidence that would prove or disprove it, or be labeled speculation.
7. Cap the loop: one rebuttal cycle by default. If positions do not change after two exchanges, stop and record the unresolved dissent.

## Compressed Rounds

Use compressed rounds by default inside normal work:

```text
Resolution:
Pro constructive:
Con constructive:
Crossfire:
Rebuttals:
Weighing:
Decision:
Preserved dissent:
```

For multi-agent HCOM work, send each role its assignment and require a short constructive plus one attack on its own side.

Read `references/termination-and-concession.md` when a debate risks looping, when agents disagree after one rebuttal cycle, or when dissent starts becoming performative.

## Output Shape

```text
Decision:
Why:
Best opposing argument:
What would flip it:
Next action:
```
