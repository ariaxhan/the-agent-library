# Catalog

Every skill, grouped by the pillar it serves. **✅ = shipped & polished.** **📋 = mapped, distillation in progress.** Each planned skill already has a working source system behind it — they're being generalized and de-branded, not invented.

Grab any shipped skill by copying its `skills/<name>/SKILL.md`. Want a planned one sooner? Open an issue and it jumps the queue.

---

## 1 · Durable memory & judgment
*Externalized judgment that compounds — agents and humans never start from zero.*

- ✅ **agent-tradition** — institutional memory layer (telos / ethos / doctrine / canon / phronesis) + a commission→chronicle work loop, hook-enforced.
- 📋 **commission-before-work** — scaffold a scope + authority + outcomes doc before substantial work, so the agent questions the premise first.
- 📋 **session-chronicle-gate** — block a session from ending until it writes an honest "what actually happened" account for the next session.
- 📋 **falsifiable-doctrine-ledger** — record team beliefs as standing bets: belief · confidence · evidence · what-would-falsify-it · review-date.
- 📋 **narrative-canon-memory** — preserve failures/breakthroughs as *stories* (context+conflict+consequence), not one-line rules, tuned for agent retrieval.
- 📋 **phronesis-recurrence-gate** — distill judgment only from patterns that recurred across multiple sessions; every entry carries its "danger of overgeneralizing."
- 📋 **agent-durable-memory-sqlite** — one zero-dependency SQLite file as an agent's cross-session memory; structure fills itself as a side effect of correct API use.
- 📋 **evidence-first-memory** — store verbatim source quotes with provenance as the primary layer; build abstractions on top, never instead.
- 📋 **session-handoff-brief** — write a structured resume doc (state / commands / failing gates / next action) before a context reset.
- 📋 **context-fidelity-compaction** — the behavioral early-warning signs that an agent's reasoning is degrading, so you compact *before* the output rots.
- 📋 **learn-graduate-prove-loop** — promote agent "learnings" from observation → hypothesis → proven rule on an evidence threshold, killing cargo-cult rules.

## 2 · Earned confidence & verification
*Nothing is good because it sounds good. Prove it beats the cheap baseline.*

- ✅ **verify-live-not-committed** — "done" means ran-it/curled-it/saw-it-pass, never inferred from a commit.
- ✅ **research-failures-first** — hunt other people's post-mortems before building; produce a symptom→cause→fix→URL map.
- 📋 **blind-evaluator-for-agent-output** — never let an agent grade its own work (self-scoring inflates ~36%); use a separate grader with fresh context.
- 📋 **metric-confound-guard** — before trusting any new metric, prove it isn't secretly measuring output length (or another confound).
- 📋 **cheap-floor-baseline-discipline** — benchmark against the strongest *cheap* baseline (the market price, the length control, the raw logits), never against chance.
- 📋 **honest-forecaster-calibration-vs-crowd** — score a predictor by Brier-delta vs the crowd, not PnL; gate autonomy on calibration, not returns.
- 📋 **earned-certainty-scorer** — separate how authoritative an output *sounds* from how much evidence backs it; flag the gap.
- 📋 **programmatic-llm-eval-harness** — benchmark models on real tasks with deterministic verifiers instead of an LLM judge.
- 📋 **honest-negative-results-archive** — document what your experiment *disproved*, including the confound that killed it.
- 📋 **headless-claude-as-benchmark-provider** — run evals against your Claude subscription via the local CLI instead of paying per-token (with the comparability caveat).

## 3 · Safe multi-agent orchestration
*Fan out work without the agents clobbering each other or lying about it.*

- 📋 **tiered-rigor-orchestration** — match process + agent topology to stakes (T1 solo / T2 orchestrate→implement→verify / T3 + adversary).
- 📋 **agent-spawn-contract** — delegate with an explicit, rejectable scope: file allowlist, tool limits, required return format.
- 📋 **parallel-agent-worktree-isolation** — run N coding agents in parallel in isolated git worktrees; discard failures by deleting the worktree.
- 📋 **verify-by-file-not-receipt** — a sub-agent's summary is intent; only the file on disk is evidence. Open it before marking done.
- 📋 **subagents-must-write-to-files** — every sub-agent persists its findings to a known path before returning, so async context never evaporates.
- 📋 **coordination-bugs-over-code-bugs** — review parallel work for file-overlap and scope-drift *first*; coordination failures dominate code bugs ~4.3×.
- 📋 **parallel-first-with-evidence** — default to parallel for independent work, serialize on shared files — with a logged trail of when "always parallelize" got burned.

## 4 · Mechanical enforcement & safety
*If it must hold, a hook holds it.*

- ✅ **rules-need-hooks-not-prose** — split rules into skeleton (hook-enforced) vs judgment (methodology); prose rules fail ~40% under load.
- ✅ **runaway-agent-killswitch** — count+duration cap on autonomous loops; fail-open, PreToolUse-not-Stop, sweep-stale-on-start.
- 📋 **investigate-before-mutating** — before any rm/mv/reset on something you didn't create this session, verify what it is; an empty folder is a signal, not junk.
- 📋 **single-source-of-truth-generation** — generate an asset and its machine spec from one definition so the image and the coordinates can't drift.
- 📋 **store-readiness-ship-no-ship-gate** — one command fans out parallel pre-release audits into a single SHIP / NO-SHIP verdict.

## 5 · LLM pipelines
*Wrap the probabilistic core in a deterministic honesty layer.*

- 📋 **hybrid-deterministic-plus-llm-extraction** — LLM does judgment, code does the math, schema validates everything. For trustworthy document extraction.
- 📋 **entropy-guided-document-extraction** — cheap Shannon-entropy + compression pre-filters drop boilerplate before the expensive model call.
- 📋 **discover-dont-classify** — make a document pipeline domain-agnostic by clustering to find the target, instead of hardcoding categories.
- 📋 **thompson-sampling-agent-runtime** — wrap an agent in a bandit loop that auto-routes among config "arms" by measured reward, no retraining.
- 📋 **website-technical-correctness-policy-engine** — enforce that rendered pages actually carry their JSON-LD/hreflang/canonical — and that structured data didn't silently drop facts.
- 📋 **spec-as-product-compiler** — architect generative tooling so the LLM fills validated slots in an IR, instead of emitting the final artifact directly.

## 6 · Build & ship discipline
*Headless, reproducible, honest about effort.*

- ✅ **ship-ios-to-testflight-keyonly** — iOS + macOS Catalyst to TestFlight with an ASC API key only, fully headless.
- 📋 **estimate-in-agent-hours** — quote builds in active AI-session hours, not contractor calendar-days (~3–5× compression); the unit changes the decision.
- 📋 **demand-gated-build-discipline** — phase gates that stop an eager agent from building product layers before demand is proven.
- 📋 **delegate-provisioning-to-a-non-technical-operator** — wrap a multi-step deploy in a skill a non-dev runs by answering 3 questions; hide all the git ceremony.

## 7 · Research & knowledge ops
*Turn reading, thinking, and note-keeping into a self-correcting system.*

- 📋 **knowledge-distillation-pipeline** — scrape → distill → weave → collide → graduate, as discrete skills over a notes vault.
- 📋 **provenance-capture-inbox** — capture sources verbatim with mandatory attribution; defer all classification to a later pass.
- 📋 **knowledge-decay-gardener** — score notes on age + access and archive/promote on a forgetting curve so the store doesn't silt over.
- 📋 **research-build-bridge** — keep a thinking-repo and a code-repo honestly in sync via one seam file with explicit crossing rules.
- 📋 **specimen-vault-experiment-archive** — immutable, timestamped, SQL-queryable experiment records; a zero-infra alternative to MLflow/W&B.
- 📋 **falsifiable-experiment-chamber-spec** — design research experiments as falsifiable units that each isolate one failure mode against a baseline.
- 📋 **narrowest-scope-placement-convention** — keep a sprawling config tree from re-sprawling: content lives at the narrowest scope that breaks if it's wrong.

## 8 · Creative systems
*Bottle taste and turn output into an operated engine.*

- ✅ **humanize-ai-prose** — seven ordered passes from AI-slop to human writing; structure for detectors, word-level for humans.
- ✅ **train-a-taste-model** — frozen backbone + tiny head trained on pairwise preferences from your own implicit curation signals.
- 📋 **voice-system-from-own-corpus** — derive a personal-voice editing system empirically from your own before/after drafts, not hand-written style rules.
- 📋 **daily-content-engine** — an idea→draft→publish→learn pipeline as staged folders with an explicit human/automation boundary.
- 📋 **bank-model-content-inventory** — maintain content as a categorized bank of ready pieces instead of a deadline calendar.
- 📋 **bandit-engagement-learner** — score each published piece and update Bayesian priors over hooks/topics so generation drifts toward what works.
- 📋 **cited-collision-newsletter** — an automated digest whose moat is cited cross-domain collisions, gated against hallucination (≥3 verified sources).
- 📋 **hackathon-win-system** — an evidence-ranked win-condition rubric + pre-event checklist + a "what will 80% build? invert it" entropy scan.
- 📋 **paper-to-epub-pipeline** — programmatically convert research PDFs into clean, accessible EPUBs.
