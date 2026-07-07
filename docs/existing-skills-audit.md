# Existing Skills Audit

Date: 2026-06-25

Method: [skill-methodology.md](./skill-methodology.md). This audit records the first high-priority packaging pass.

## Packaged In This Pass

| Source skill | Packaged skill | Category | Output | Packaging notes |
|---|---|---|---|---|
| `skill-creator` / repo methodology | [`create-portable-skill`](../skill-craft/create-portable-skill) | Skill craft | Portable skill folder + catalog decision | Added because the repo needs its own skill for making skills. |
| `tradition-commission` | [`commission-work`](../work-management/commission-work) | Work management | Commission document | Rewritten to avoid hard dependency on local `_meta`, hooks, AgentDB, or canon. |
| `tradition-chronicle` | [`write-session-chronicle`](../work-management/write-session-chronicle) | Work management | Chronicle document | Rewritten as a portable wrap-up workflow with optional project conventions. |
| `vaults-hunt` | [`hunt-research-sources`](../research-notes/hunt-research-sources) | Research & notes | Ranked findings report | Rewritten with generic output paths and no Vaults-only folders. |
| `vaults-extract` | [`extract-source-to-notes`](../research-notes/extract-source-to-notes) | Research & notes | Structured source note | Rewritten to include capture/distill/collision steps instead of delegating to local helper skills. |
| `vaults-autonomous` | [`forge-autonomous-work`](../process-engines/forge-autonomous-work) | Process engines | Code changes plus iteration log, or escalation record | Merged into Forge during the cognition-consolidation pass as acceptance mode. |
| `vaults-vision-handoff` | [`write-project-vision-handoff`](../planning-handoff/write-project-vision-handoff) | Planning & handoff | `VISION.md`, `FLOWCHARTS.md`, optional supplementary docs | Bundled `reference/templates-and-examples.md`. |
| `vaults-vision-critique` | [`critique-vision-handoff`](../planning-handoff/critique-vision-handoff) | Planning & handoff | Severity-rated critique with concrete fixes | Bundled `reference/techniques-and-output.md`. |

## Kernel Command Extraction

These are the point of the repo: standalone process engines, generalized from kernel commands.

| Source command | Packaged skill | Category | Output | Generalization |
|---|---|---|---|---|
| `/kernel:forge` | [`forge-autonomous-work`](../process-engines/forge-autonomous-work) | Process engines | Artifact, evidence log, stress-test result, final verdict | Removed AgentDB/kernel command requirements; kept heat/hammer/quench/temper/anneal loop. |
| `/kernel:dream` | [`dream-solution-space`](../process-engines/dream-solution-space) | Process engines | Competing perspectives, council critique, integrity scores, recommendation | Removed codebase-only assumptions; kept grounded divergence + stress test. |
| `/kernel:experiment` | [`experiment-on-rules`](../process-engines/experiment-on-rules) | Process engines | Hypotheses, experiment designs, evidence, confidence updates, rule recommendations | Removed AgentDB requirement; kept rule-as-hypothesis engine. |

## Code Engineering (standalone)

Code skills are one category, not the whole repo. Each is **standalone**: it works copied on its own, with no dependency on a parent system, local AgentDB, hooks, or sibling skills. (Originally derived from `kernel-claude` methodology, then de-coupled.)

| Source skill | Packaged skill | Category | Output | Generalization |
|---|---|---|---|---|
| `debug` | [`debug-code-systematically`](../code-engineering/debug-code-systematically) | Code engineering | Reproduction, root cause, fix, regression check | Removed AgentDB/kernel assumptions; kept scientific debugging flow. |
| `refactor` | [`refactor-code-safely`](../code-engineering/refactor-code-safely) | Code engineering | Behavior-preserving refactor with before/after checks | Removed project tiering/commit rules; kept scope audit and transformation discipline. |
| `quality` | [`review-ai-code-quality`](../code-engineering/review-ai-code-quality) | Code engineering | Prioritized code quality findings | Generalized Big Five review for AI-authored code. |
| `api` | [`design-api-contracts`](../code-engineering/design-api-contracts) | Code engineering | API contract and checklist | Kept REST contract guidance; made framework-neutral. |
| `security` | [`secure-code-changes`](../code-engineering/secure-code-changes) | Code engineering | Security checklist, findings, fixes | Kept sensitive-surface review; removed local tool assumptions. |
| `orchestration` | [`orchestrate-coding-agents`](../code-engineering/orchestrate-coding-agents) | Code engineering | Scoped agent contracts and merge/verification protocol | Removed AgentDB requirement; kept contract/isolation/verification workflow. |

## Already Packaged Before This Pass

| Skill | Category | Call |
|---|---|---|
| [`humanize-ai-prose`](../creative-taste/humanize-ai-prose) | Creative & taste systems | Keep. Ordered editing workflow with companion checklist. |
| [`train-a-taste-model`](../creative-taste/train-a-taste-model) | Creative & taste systems | Kept. Niche, but it exists on disk and remains cataloged. |

## Still Draft

| Skill | Category | Needed |
|---|---|---|
| [`build-and-release-ios-app`](../shipping/build-and-release-ios-app) | Shipping | Expand from ASC-key TestFlight upload into full lifecycle: design/import, native build, tests, metadata, screenshots, TestFlight, App Review. |

## Operating-Pattern Skills

| Entry | Current home | Reason |
|---|---|---|
| [`agent-tradition`](../operating-patterns/agent-tradition) | Operating patterns | Agent operating system skill. Related workflows are also packaged separately. |
| [`research-failures-first`](../operating-patterns/research-failures-first) | Operating patterns | Methodology-shaped skill for implementation research. |
| [`harden-rules-into-hooks`](../operating-patterns/harden-rules-into-hooks) | Operating patterns | Enforcement-pattern skill. |

## Non-Coder Pass (2026-06-26)

Reframed the whole library for a general (non-coder) audience. Deleted `train-a-taste-model`. Kept the six code skills but reframed them as standalone (not a kernel-derived system). Mined the broader body of work (tradition, kernel commands, CollabVault, chronicles, experiments) for proven, generalizable *process* patterns, then built the first wave.

Built this pass:

| Skill | Category | Source / evidence |
|---|---|---|
| `reality-audit` | Verify & review | the "verified live" lesson: the most-repeated pattern across the source body of work |
| `test-the-measuring-stick` | Verify & review | cheap-floor / dummy-answer precedents (a content-free answer beat every model on a real eval) |
| `audit-the-premise` | Verify & review | the investigation-first principle (false-premise tasks caught by reading reality first) |
| `fresh-eyes-adversary-pass` | Verify & review | Merged into `reality-audit` during the cognition-consolidation pass; same audit engine, different entry mode. |
| `brainstorm-with-entropy` | Process engines | an entropy-injection brainstorming workflow (8 named techniques) |
| `synthesize-learnings` | Work management | a cross-session retrospective + the recurrence-based promotion gate |
| `manage-a-knowledge-base` | Research & notes | a personal-knowledge-base family (triage / collide / weave / curate / decay / integrity) as one 6-phase kit |

Rules folded into skills (not shipped as standalone skills or a separate pack): verify-live and root-cause-the-class → `reality-audit`; reliability≠value and cheap-floor → `test-the-measuring-stick`; investigate-before-mutating / restore-in-place → `audit-the-premise`; recurrence-not-excitement → `synthesize-learnings` + the kit.

## Next Packaging Work

1. Build the mapped second wave (see CATALOG "Mapped, Not Yet Built").
2. Expand [`build-and-release-ios-app`](../shipping/build-and-release-ios-app).
3. Audit `secure-keys` for a publishable credential-audit skill.
