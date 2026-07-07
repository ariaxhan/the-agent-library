---
name: delegate-to-worker-models
description: >-
  Delegate implementation to cheap or small models safely by pre-deciding everything.
  Use when splitting work across agent lanes, picking a model tier, or writing a worker
  prompt: "can a small model do this", "delegate this", "fan this out", "spawn workers
  for these", "which model for this task". Encodes the lane contract template, the
  pre-verified guide requirement, and the honest track record of where cheap models
  succeed and where they quietly fail.
---

# Delegate to Worker Models

Cheap models are not junior engineers; they are excellent typists. Observed across
production agent runs, small models are reliable in exactly two roles: **total-spec
execution** (every decision already made, written down, and verified) and **mechanical,
evidence-only verification** (run these commands, report the raw output). Everywhere they
were handed a decision, they drifted: inventing spec where the prompt was silent, or dying
on a trap the coordinator knew about but did not restate. The wins are a decomposition
achievement, not a model achievement: the coordinator pre-deciding everything is what makes
cheap models safe.

## The two safe jobs, and the tell

- **Total-spec execution**: the lane implements a written guide with zero open questions.
- **Evidence-only verification**: the lane runs named checks and returns raw output, never
  a judgment.

The tell: if the prompt needs the phrase "use your judgment" anywhere, it is a strong-model
task. Do not lengthen the prompt to compensate; change the model or make the decision
yourself first.

## The pre-verified guide (a lane is only as safe as its guide)

Before delegating anything non-mechanical, write a guide the lane executes. Every API
signature in it is grepped from the installed package source (the type declarations on
disk) the day the guide is written, never recalled from memory: recall is the hallucination
risk, in the guide author as much as in the lane. Name the repo conventions with a concrete
file to copy from. A lane without a guide is a coin flip; a lane with one lands green.

## The lane contract (every section is load-bearing)

1. **One deliverable, named.** Never two features.
2. **Read-first list, ordered.** The guide, then the 2 to 4 existing files whose patterns
   get copied, by exact path. State that the guide wins every conflict.
3. **Files table.** CREATE vs MODIFY, exact paths. A lane that invents a path is off-contract.
4. **Known traps, restated.** Even if they are documented elsewhere. Lanes have died on
   traps that were written down one file away. Repetition is cheap; rediscovery is not.
5. **Verification loop with exact commands and expected counts** ("111 existing plus your
   12 new"). "Iterate until green", never "run the tests".
6. **Forbidden list.** No commits (the coordinator commits), no dependency or lockfile or
   config changes, no files outside the table, explicit limits on sensitive scopes.
7. **Return format: raw data.** Files with line counts, test-output tails, deviations with
   one-line reasons, and "what the coordinator should adversarially probe". Never accept
   narrative alone.

## Coordinator duties after a lane returns

- **Re-run the gate yourself.** The lane's output is a claim, not evidence. Across
  production runs, lane reports are wrong or importantly incomplete roughly 1 in 5 times.
- **Diff-read the actual changes** and check the forbidden list held: no stray files, no
  touched dependencies or contracts.
- **Commit yourself**, with a conventional message. Lanes never commit.

## When a lane fails or is cancelled

Harvest before disposal: extract the trap that killed it into the guide, archive the tree
if you want the reference, then **reimplement fresh from the improved guide**. Never merge
the corpse because most of it passed; the guide is now worth more than the code, and fresh
execution from it is faster than debugging a half-dead branch.

## Anti-patterns

- **Delegating a decision to a cheap model.** It will make one, silently, and the spec drifts.
- **A guide written from memory.** Grep the installed source; recalled signatures are the bug.
- **Trusting "all tests pass" from a lane.** Counts from your own shell only.
- **Omitting a trap because "it's in the docs".** Restate it in the contract.
- **Merging a cancelled lane's branch to save time.** Harvest the trap, reimplement fresh.

## Output

Return, per delegation: the model tier with the reason (which of the two safe jobs it is),
the guide path, the full lane contract, and after return: the coordinator's own gate run,
the diff-read result, and the commit.
