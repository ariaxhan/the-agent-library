---
name: experiment-on-rules
description: Treat prompts, rules, workflows, habits, or methodology claims as hypotheses and test them with evidence. Use when the user asks to "run an experiment", "prove this rule", "test this methodology", "validate this workflow", "is this actually working", or decide whether to keep, change, or kill an operating rule. Produces hypotheses, experiment designs, evidence, confidence updates, and recommendations.
---

# Experiment On Rules

Rules without evidence are superstitions with formatting. This skill turns an operating belief into a hypothesis, tests it, and updates confidence.

Use for AI workflows, writing processes, coding rules, research habits, team norms, prompt patterns, review methods, or automation policies.

## 1. Sense the state

Collect candidate rules or claims from:

- Existing instructions
- Repeated user preferences
- Team/process docs
- Prior failures
- Current workflow assumptions
- Quantitative claims

If no explicit rule exists, extract one from behavior: "We seem to believe X helps Y."

## 2. Seed hypotheses

Convert each rule into a falsifiable statement:

```text
If we do X in context Y, outcome Z improves because of mechanism M.
```

Each hypothesis needs:

- ID
- Statement
- Source
- Domain
- Expected effect
- What would support it
- What would refute it
- Initial confidence

If no observation could refute it, rewrite it.

## 3. Pick the next hypothesis

Prioritize:

1. Most uncertain
2. Highest impact
3. Least tested
4. Easiest ethical/safe test

Do not test everything at once.

## 4. Design the lightest experiment

Choose one:

- **Historical:** query prior work, logs, notes, commits, or outcomes.
- **Comparative:** run similar tasks with and without the rule.
- **Ablation:** deliberately remove the rule in a safe context and observe.
- **Observational:** tag future tasks and collect evidence passively.

Define before running:

- Method
- Measurement
- Control condition
- Support criteria
- Refute criteria
- Minimum sample size
- Safety limits

## 5. Run and record evidence

Capture raw observations:

- Counts
- Timings
- Error rates
- Rework
- Quality scores
- User corrections
- Concrete examples
- Confounds

Never fabricate missing evidence. If the experiment cannot run, mark it inconclusive and say why.

## 6. Conclude

Verdicts:

- **Supports:** evidence clearly aligns
- **Refutes:** evidence clearly contradicts
- **Inconclusive:** evidence is weak, noisy, or confounded

Update confidence:

- Supporting evidence raises confidence.
- Refuting evidence lowers confidence.
- Inconclusive evidence records learning without changing much.

Do not modify the hypothesis after seeing results. Write a new mutated hypothesis instead.

## 7. Evolve the ruleset

Recommend:

- Graduate: keep and strengthen the rule
- Kill: remove or stop following it
- Mutate: rewrite into a sharper hypothesis
- Observe: gather more passive evidence

Human approval is required before changing important standing instructions.

## 8. Report

Return:

- Hypothesis tested
- Experiment design
- Evidence
- Verdict
- Confidence change
- Recommended rule change
- Remaining uncertainty
