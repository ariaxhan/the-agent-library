# Catalog

Every top-level folder is a category shelf. A skill is any child folder with a `SKILL.md`. Most skills are for general agent use (thinking, deciding, verifying, researching, writing, running work) across Claude, Codex, and other AI agents. Coding skills are one category, and each stands alone.

## Verify & Review

The spine of the library: how to trust AI work instead of believing its "done."

| Skill | Use it when |
|---|---|
| [`reality-audit`](./verify-and-review/reality-audit) | A done report or near-final artifact needs corroboration, defect hunting, and a ship/hold verdict. |
| [`test-the-measuring-stick`](./verify-and-review/test-the-measuring-stick) | You're trusting a score, grade, or ranking, especially an AI grading its own output. |
| [`audit-the-premise`](./verify-and-review/audit-the-premise) | A task assumes something is broken/true/decided before you act on it. |
| [`verify-adversarially`](./verify-and-review/verify-adversarially) | Work needs to earn "done": a fresh-context agent attacks it, a coordinator adjudicates every finding. |

## Process Engines

Standalone, general-purpose loops for making Claude work better.

| Skill | Use it when |
|---|---|
| [`forge-autonomous-work`](./process-engines/forge-autonomous-work) | Take substantial work end to end with competing approaches, runnable acceptance loops, stress tests, and learning. |
| [`dream-solution-space`](./process-engines/dream-solution-space) | Expand and stress-test possible approaches before committing to one. |
| [`brainstorm-with-entropy`](./process-engines/brainstorm-with-entropy) | Generate genuinely novel ideas, ranked by surprise instead of safety. |
| [`experiment-on-rules`](./process-engines/experiment-on-rules) | Treat rules, prompts, habits, or workflows as hypotheses and test them with evidence. |
| [`debate-decisions`](./process-engines/debate-decisions) | Use structured debate formats for non-trivial decisions, reviews, governance, and live disagreement. |
| [`delegate-to-worker-models`](./process-engines/delegate-to-worker-models) | Split work across agent lanes or hand implementation to a cheap model, with the lane contract and honest track record. |

## Planning & Handoff

| Skill | Use it when |
|---|---|
| [`write-project-vision-handoff`](./planning-handoff/write-project-vision-handoff) | Turn planning context into `VISION.md` and `FLOWCHARTS.md` for implementation. |
| [`critique-vision-handoff`](./planning-handoff/critique-vision-handoff) | Stress-test a handoff, spec, architecture brief, or seed document before implementation. |
| [`decompose-by-verification-boundary`](./planning-handoff/decompose-by-verification-boundary) | Split substantial work into units that each carry their own gate, ordered by risk. |
| [`hand-off-before-context-death`](./planning-handoff/hand-off-before-context-death) | Pause or end a session by writing the handoff while the verified context is still loaded. |

## Work Management

| Skill | Use it when |
|---|---|
| [`commission-work`](./work-management/commission-work) | Shape substantial work into authority, boundaries, outcomes, and checks before execution. |
| [`write-session-chronicle`](./work-management/write-session-chronicle) | Record what changed, failed, was checked, and remains after substantial work. |
| [`synthesize-learnings`](./work-management/synthesize-learnings) | Distill accumulated notes and lessons across many sessions into durable insight. |
| [`keep-a-confidence-ledger`](./work-management/keep-a-confidence-ledger) | Subsystem state needs one honest map: four evidence-backed states, no percentages. |

## Research & Notes

| Skill | Use it when |
|---|---|
| [`hunt-research-sources`](./research-notes/hunt-research-sources) | Run a broad source hunt and produce ranked findings, conflicts, rejections, and gaps. |
| [`extract-source-to-notes`](./research-notes/extract-source-to-notes) | Process one URL, paper, article, transcript, or pasted source into structured notes. |
| [`manage-a-knowledge-base`](./research-notes/manage-a-knowledge-base) | Run a notes vault / second brain as a system: triage, connect, synthesize, curate, decay, audit. (Kit: 6 phases.) |

## Creative & Taste

| Skill | Use it when |
|---|---|
| [`humanize-ai-prose`](./creative-taste/humanize-ai-prose) | Revise AI-shaped writing into specific, human prose. |
| [`train-a-taste-model`](./creative-taste/train-a-taste-model) | Train a small model on your own archive that ranks new items the way you would, from curation signals you already produced. |

## Skill Craft

| Skill | Use it when |
|---|---|
| [`create-portable-skill`](./skill-craft/create-portable-skill) | Create, audit, classify, or package a portable Claude/Codex skill. |

## Code Engineering

Standalone coding skills. Each works on its own: copy just the one you need; none depend on the others or on a parent system.

| Skill | Use it when |
|---|---|
| [`debug-code-systematically`](./code-engineering/debug-code-systematically) | Reproduce, isolate, and fix a bug from root cause. |
| [`refactor-code-safely`](./code-engineering/refactor-code-safely) | Clean, rename, move, extract, inline, or simplify code without behavior drift. |
| [`review-ai-code-quality`](./code-engineering/review-ai-code-quality) | Review AI-authored or recent code for validation, edge cases, errors, duplication, and complexity. |
| [`design-api-contracts`](./code-engineering/design-api-contracts) | Design or review REST/API contracts, errors, pagination, versioning, and agent-facing endpoints. |
| [`secure-code-changes`](./code-engineering/secure-code-changes) | Review or implement sensitive code touching auth, secrets, permissions, inputs, payments, or PII. |
| [`orchestrate-coding-agents`](./code-engineering/orchestrate-coding-agents) | Split coding work across agents with scoped contracts, isolation, and verification. |
| [`secure-keys`](./code-engineering/secure-keys) | Audit how your AI tools and agents hold API keys: find exposed keys, move connections to OAuth, migrate the rest to secure storage with runtime lookups, then rotate and scope. |
| [`build-sites-as-specs`](./code-engineering/build-sites-as-specs) | Architect a site generator that can't produce slop: compile a validated spec into output instead of generating HTML, so quality becomes policies the model can't bypass. |
| [`design-loud-failures`](./code-engineering/design-loud-failures) | Design or review any computation humans act on so a failure can never present as success: named invariants, explicit skip states, honest cause classes, loud no-answer results. |

## Shipping

| Skill | Use it when |
|---|---|
| [`audit-website-quality`](./shipping/audit-website-quality) | Audit any site before launch against the full policy bank (SEO, a11y, performance, responsive, security, anti-slop content, links, structured data) with graded findings. |
| [`prep-site-for-ai`](./shipping/prep-site-for-ai) | Make a site legible to LLMs, AI search, and agents: structured data, llms.txt, server-rendered facts, crawler access, provenance, so AI quotes you right instead of guessing. |
| [`build-and-release-ios-app`](./shipping/build-and-release-ios-app) | Draft. Current body covers ASC-key TestFlight upload; needs full release lifecycle. |

## Operating Patterns

| Skill | Use it when |
|---|---|
| [`agent-tradition`](./operating-patterns/agent-tradition) | Install or understand durable agent memory, commissions, chronicles, and accountability hooks. |
| [`research-failures-first`](./operating-patterns/research-failures-first) | Research real-world failure modes before non-trivial implementation. |
| [`harden-rules-into-hooks`](./operating-patterns/harden-rules-into-hooks) | Turn important agent/process rules into enforceable hooks or checks. |
| [`extend-before-inventing`](./operating-patterns/extend-before-inventing) | You're about to create a file, helper, wrapper, or system: find and extend the existing spine first. |

## Mapped, Not Yet Built

Proven patterns from real work, queued for a later wave (each has source evidence; not yet packaged):

- **Verify & review:** `sweep-for-silent-failures`, `flag-dont-guess`, `bake-off-the-tool`, `test-the-judges-exact-flow`
- **Thinking & deciding:** `stretch-an-idea`, `weigh-the-options`, `diagnose-before-fixing`
- **Work management:** `manage-the-context-window`
- **Creative & taste:** `match-a-defined-voice` (build-your-own voice system)
- **Research & notes:** `daily-linked-news-brief`, `load-project-context`
