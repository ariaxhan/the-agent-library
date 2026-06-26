---
name: brainstorm-with-entropy
description: Generate genuinely novel ideas by injecting entropy, ranked by surprise instead of safety. Use when the user asks to brainstorm, generate ideas, find an angle, or name something — "what could I build/make/write", "I need fresh ideas", "help me think of", "I'm stuck on the obvious options". Triggers also include "brainstorm with me" and "give me something unexpected". Produces a ranked list of ideas, each tagged with the technique that produced it, its core insight, its risk, and a cheap validation signal.
---

# Brainstorm with Entropy

Ordinary brainstorming converges on the obvious because it optimizes for what's safe. This does the opposite: it forces distance from the first answer using named techniques, then ranks by novelty so the strange ideas survive long enough to be considered.

The output is range, not a single safe pick. Converge later, on request.

## 1. Extract the constraints

Pin down before generating:

- **Domain** — what space are we in.
- **Goal** — what a win looks like.
- **Hard limits** — budget, time, audience, non-negotiables.
- **Anti-goals** — what it must *not* be. These matter as much as the goal; they're what keep the ideas from collapsing back to the obvious.

## 2. Inject entropy with named techniques

Use at least two. Naming the technique lets the user say "more like that."

| Technique | How to apply it |
|---|---|
| Inversion | Solve the opposite problem, then flip the answer back. |
| Domain-collision | Borrow the mechanism from an unrelated field and force-fit it here. |
| Constraint-flip | Remove the constraint everyone assumes, or add an absurd one. |
| Scale-shift | Do it for 1 person, then for 10 million. What changes? |
| Audience-swap | Build it for the wrong audience — a child, an expert, an enemy. |
| Time-warp | How would this be done in 1900? In 2100? |
| Subtraction | Remove the most "essential" part. What's left? |
| Analogy-mining | "This is like ___" — chase the analogy to its consequences. |

## 3. Generate 5–10 ideas in a fixed shape

Each idea:

- **Name** — a memorable handle.
- **Pitch** — one line.
- **Core insight** — why it could work.
- **Source** — which technique or collision produced it.
- **Risk** — the main reason it might fail.
- **Cheap signal** — the smallest test that would validate or kill it.

Force at least one idea that makes you wince or laugh. If nothing's uncomfortable, you haven't added enough entropy.

## 4. Rank by entropy, not feasibility

Order the list by novelty and surprise — the distance from the obvious answer — not by how safe or buildable each is. Ranking by feasibility quietly re-sorts the safe idea back to the top and defeats the whole exercise.

## 5. Converge only when asked

Offer to narrow to the most promising candidates, but don't collapse to the comfortable option by default. Let the user pull the lever from divergence to convergence.

## Output

Return:

- A ranked idea list (most novel first), each in the Name / Pitch / Insight / Source / Risk / Signal shape.
- The techniques used, so the user can ask for more from a specific one.
- Optionally, the list appended to an idea-bank file for later.
