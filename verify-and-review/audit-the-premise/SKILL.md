---
name: audit-the-premise
description: Stress-test the assumption baked into a task before spending real effort on it. Use when a request asserts something is broken, true, already decided, or unchanged before you act on it — "fix the broken X", "since Tuesday it's been down", "just flip the existing thing", "the data already has Y". Triggers include "is this problem even real", "check the assumption before I start", "the request says X but is that true". Produces a confirmed-or-corrected understanding, a logged disagreement when the premise was wrong, and a safer revised plan.
---

# Audit the Premise

Most tasks arrive with a hidden claim attached — that something is broken, that a fact holds, that the fix is small. Act on the claim and you can spend hours solving a problem that was never real, or confidently break something that was fine. This checks the claim first.

Scale it to stakes: skip it for trivial, well-specified asks; always run it before anything hard to undo.

## 1. Treat the framing as a hypothesis

Before doing anything, ask the one question that collapses wasted work:

> What single thing, if false, makes this whole task pointless?

Name that load-bearing assumption explicitly. The request is a claim about reality, not reality itself.

## 2. Check the load-bearing facts against the real state

Look at the actual current state end-to-end before changing anything:

- "It's broken" → reproduce the break yourself.
- "It's been down since Tuesday" → check when it actually changed.
- "Just flip the existing thing" → confirm the thing exists and does what's assumed.

Read-only investigation is cheap. It is what separates a safe two-line change from a confidently-broken big one.

## 3. If reality contradicts the framing, stop

The contradiction is not an obstacle — it **is** the finding. When what you see disagrees with what you were told:

- Do not silently comply and build on the false premise.
- Do not silently "fix" reality to match the request either.
- Halt and surface the gap. Never tidy, overwrite, or recreate something on a hunch that it's wrong.

## 4. Proceed on the truer question and log the disagreement

Once the real state is clear, work the actual problem — which is often smaller and different from the one asked. Write down the disagreement in three lines:

- What you were asked.
- What's actually true.
- What you did instead, and why.

A wrong assumption that never gets recorded comes back and gets believed again months later. Recording it is what stops the loop.

## 5. Revise the plan

Restate the task as it really is now. Usually it shrinks: a smaller change, a different target, or sometimes "nothing to do here — the premise was false."

## Output

Return:

- The load-bearing assumption you tested.
- What the real state turned out to be, with how you checked it.
- A disagreement note (asked / true / did instead) when the premise was wrong.
- The revised, premise-corrected plan — or a clear statement that no action is needed.
