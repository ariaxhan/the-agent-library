---
name: debate-decisions
description: >-
  Ambient structured debate protocols for decision-making, architecture tradeoffs, code
  review, research synthesis, safety analysis, governance, prioritization, and any moment
  where Codex is choosing, recommending, reviewing, approving, or weighing competing
  options. Use implicitly at decision points even when the user does not say "debate":
  when a task has multiple plausible paths, high impact, disagreement risk, unclear
  values, policy/doctrine implications, or benefits from adversarial review. Provides
  Public Forum, Congressional Debate, Lincoln-Douglas, Policy, World Schools, Big
  Questions, and Extemporaneous Debate patterns.
---

# Debate Protocols

Use speech-and-debate formats as thinking machinery. Do not wait for the user to say "debate." If the work contains a real choice, a review judgment, a governance call, or a high-impact recommendation, silently choose the smallest useful debate pattern and run it in compressed form.

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
2. Assign sides before arguing. If there are multiple agents, randomize sides or make the stronger model argue the side it is less likely to believe.
3. Treat assigned side as a role, not belief.
4. Require constructive cases before rebuttal.
5. Force direct clash: questions must target the live weak point, not vibes.
6. End with a decision record: winner, strongest argument, unresolved risk, evidence that would flip the result, and preserved dissent.
7. Do not let debate replace deterministic evidence. If grep, tests, logs, or source files can decide, use them as the judge.

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

## Output Shape

```text
Decision:
Why:
Best opposing argument:
What would flip it:
Next action:
```
