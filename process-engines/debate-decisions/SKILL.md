---
name: debate-decisions
description: >-
  Ambient structured debate protocols for non-trivial decision-making, architecture
  tradeoffs, code review, research synthesis, safety analysis, governance, and
  prioritization. Use implicitly at decision points even when the user does not say
  "debate" when a task is high-impact, hard to reverse, doctrine/policy-bearing,
  multi-agent, or has live disagreement or multiple plausible paths. Skip for trivial,
  cheap-to-reverse, or deterministically decidable choices. Provides
  Public Forum, Congressional Debate, Lincoln-Douglas, Policy, World Schools, Big
  Questions, and Extemporaneous Debate patterns.
---

# Debate Protocols

Use speech-and-debate formats as thinking machinery. Do not wait for the user to say "debate." If the work contains a real choice, a review judgment, a governance call, or a high-impact recommendation, silently choose the smallest useful debate pattern and run it in compressed form.

Skip the skill when grep, tests, logs, source files, or official records can answer the question directly. Deterministic evidence is the judge; debate is only for choices evidence cannot fully settle.

## Format Picker

- **Public Forum**: use for binary decisions with two plausible sides. Default for "should we do X?"
- **Congressional Debate**: use for governance, prioritization, multi-agent synthesis, doctrine, commissions, and roadmap decisions.
- **Lincoln-Douglas**: use when the real conflict is values or principles.
- **Policy Debate**: use for complex implementation or architecture choices with plans, counterplans, and risks.
- **World Schools**: use for team strategy, collaborative synthesis, or when one side needs a clean narrative plus live objections.
- **Big Questions**: use for foundational philosophical or interpretive questions.
- **Extemporaneous Debate**: use for fast researched clash when there is not time for a full round.

Detailed format cards live in `references/`. Load only the relevant card.

## Core Rules

1. State the resolution in one sentence.
2. Assign sides before arguing. For peer agents, the proposer argues against their own proposal and the reviewer argues for it; otherwise use a coin flip or a stable hash of the resolution.
3. Treat assigned side as a role, not belief. Concession is allowed and counts as progress.
4. Require constructive cases before rebuttal.
5. Force direct clash: questions must target the live weak point, not vibes.
6. End with a decision record: winner, strongest argument, unresolved risk, evidence that would flip the result, and preserved dissent.
7. Do not let debate replace deterministic evidence. If grep, tests, logs, or source files can decide, use them as the judge.
8. Make every dissent testable. An objection must name the evidence that would prove or disprove it, or be labeled speculation.
9. Cap the loop: one rebuttal cycle by default. If positions do not change after two exchanges, stop and record the unresolved dissent.

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
