---
name: extract-invariants
description: >-
  Turn a borrowed metaphor, analogy, or cross-domain inspiration into a testable mechanism, or prove it is decoration and discard it. Use when a design leans on language from another field ("immune system", "evolution", "market", "quorum", "crystallization"), when someone proposes copying how another domain solves a problem, or when reviewing a system whose names sound deeper than its code. Produces either a named domain-free invariant with evidence and falsifiers, or an explicit rejection with the reason it failed.
---

# Extract Invariants

Metaphors are how good ideas travel between domains, and also how decorative complexity sneaks into systems. The failure mode is consistent: a compelling name ("immune memory", "pheromone trails", "energy minimization") gets an API before anyone checks whether a distinct mechanism exists under it. Months later the code performs elaborate ceremony that reduces to a cache, a counter, or nothing at all.

This skill is the gate. A borrowed idea passes only as a domain-free mechanism; the vocabulary it arrived in never ships.

## The test in one line

If the idea still needs its source-domain noun to sound meaningful, it has not been abstracted yet.

## 1. State the phenomenon plainly

Write down what the source system actually does, in the source domain's own terms. One paragraph. No implications for your system yet.

Example: "Black holes have event horizons: regions where causal influence flows in one direction only."

## 2. Strip every domain noun

Rewrite the phenomenon with all source-specific vocabulary removed. Every noun must be generic: boundary, log, score, budget, gate, copy, signal, decay.

- "Event horizon" becomes "an irreversible causal boundary: information may cross in one direction and never back."
- "Immune memory" becomes "a pattern store keyed by past attacks, with faster response on re-encounter and gradual decay."
- "Pheromone trail" becomes "a shared score that successful paths increment and time decays."

If the rewrite says nothing, stop: you had a mood, not a mechanism. Record the rejection and why.

## 3. Extract the smallest invariant

Reduce the stripped description to the minimal relationship that must hold, plus its necessary conditions. Ask: what is the smallest claim that, if false, kills the idea?

Format:

- **Invariant**: the domain-free claim.
- **Necessary conditions**: what must be true of any system for the invariant to apply.
- **Tradeoffs**: what enforcing it costs.
- **Failure modes**: how systems that rely on it break.

## 4. Demand independent recurrence

One domain is an anecdote. Search for the same invariant, independently evolved, in at least two unrelated domains (biology and markets; distributed systems and law; ecology and open source). Kill rule: no recurrence across genuinely unlike domains within a bounded search, then classify it as an interesting metaphor and stop.

Recurrence is the evidence. Convergent evolution under similar constraints is what separates an organizational law from a poetic resemblance.

Beware the near-miss: two domains that share ancestry (two internet communities, two mammal species) are one domain for this test.

## 5. Check it is operational and falsifiable

A surviving candidate must answer all three:

- **Instantiation**: what is the smallest software or process change that implements it? Name the concrete primitive (append-only log, quarantine boundary, expiring authority, reputation score, selection loop).
- **Falsifier**: what observation would prove it wrong or useless here?
- **Cost of being wrong**: what breaks if you adopt it and the invariant does not actually hold in your system?

No falsifier means it is faith, not design. Reject or park it.

## 6. Record the verdict either way

Write the outcome where future work will find it:

- **Admitted**: invariant, conditions, tradeoffs, failure modes, domains observed, proposed instantiation, falsifier, confidence.
- **Rejected**: the candidate, which step killed it, and the one-line reason. Rejections prevent the same metaphor from being re-excavated every quarter.

The record is the deliverable. An extraction that lives only in the conversation will be repeated, badly, by someone else.

## Worked warning: how it fails without the gate

A real system built "crystallographic structure factors" for measuring code quality: complex numbers, phase agreement, R-factors, three hundred lines. Under review, the machinery computed its elaborate score, then overrode it with the raw test-failure rate whenever the two disagreed. The metaphor had an API; the mechanism was a division. The same system's "pheromone-based coordination" scored answers by character length.

The tell in both cases: the vocabulary was doing the persuading. Strip the names and read what the code does. When the names carry the meaning, this skill was skipped.

## Anti-patterns

- **Metaphor-as-API**: naming modules after the source domain. Names should describe the mechanism (pattern-cache, decay-score), never the inspiration.
- **Recurrence by ancestry**: citing sibling domains as independent evidence.
- **Poetic invariants**: claims with no possible falsifier ("systems seek balance").
- **Batch romanticism**: importing a whole source domain at once. Invariants pass one at a time, each with its own evidence.
- **Skipping the rejection record**: unrecorded rejections guarantee re-litigation.
