---
name: write-project-vision-handoff
description: Create implementation-ready project handoff documents from planning context. Use when the user asks to "write a vision handoff", "create a seed document", "prepare this for a coding agent", "turn this plan into VISION.md", or transfer a planned system to an implementation agent. Produces VISION.md and FLOWCHARTS.md plus only directly useful supplementary docs.
---

# Write Project Vision Handoff

Turn planning context into documents a coding agent can build from without seeing the original conversation.

You are a planner, not the implementer. Capture intent, constraints, decisions, rejected alternatives, and success criteria. Defer exact code structure and implementation choices unless the user explicitly decided them.

## 1. Gather the source context

Read the conversation, notes, brief, screenshots, or spec the user supplied. Extract:

- Explicit decisions
- Rejected alternatives
- Hard constraints and anti-requirements
- User intent signals, including repeated frustrations or preferences
- Edge cases and failure modes already discussed
- Success criteria and launch boundaries

If the source is thin, write the missing assumptions as open questions instead of inventing facts.

## 2. Separate audiences

Write two different documents:

| Document | Audience | Purpose |
|---|---|---|
| `VISION.md` | Coding agent | Dense source of truth: what, why, constraints, decisions, task |
| `FLOWCHARTS.md` | Human reader | Plain-English architecture explanation with diagrams and glossary |

Do not duplicate sections between them. `VISION.md` carries rationale. `FLOWCHARTS.md` carries comprehension.

## 3. Write `VISION.md`

Include:

- What this is
- The problem
- The solution
- Key decisions with rationale and rejected alternatives
- Design constraints
- Anti-requirements
- Planning considerations
- Success criteria
- The coding agent's task

Rules:

- No code or pseudocode.
- No file trees unless already decided.
- No library/framework prescriptions unless already decided.
- Preserve user quotes when they capture intent better than a summary.

## 4. Write `FLOWCHARTS.md`

Include:

- Core concept in simple language
- Glossary for technical/domain terms
- ASCII flow diagram
- Scenario walkthroughs
- Component breakdown
- Questions to verify understanding

Every technical term gets a plain-English definition. Prefer diagrams over paragraphs.

## 5. Add supplementary docs only when needed

Allowed:

- `DECISIONS.md` for many complex tradeoffs
- `CONSTRAINTS.md` for unusual technical or business limits
- `PRIOR_ART.md` for existing systems the plan references
- `GLOSSARY.md` when domain vocabulary is heavy

Do not create README, installation docs, changelog, or implementation guides.

## 6. Validate the handoff

Before finishing, check:

- Could a coding agent build from this without the original conversation?
- Are all decisions and rejected alternatives captured?
- Are constraints sourced and not invented?
- Are success criteria observable?
- Could a non-technical person understand `FLOWCHARTS.md`?
- Is there zero meaningful overlap between the two documents?

Use `reference/templates-and-examples.md` for templates and examples when writing the files.
