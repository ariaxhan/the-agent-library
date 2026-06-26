---
name: commission-work
description: Create or refine a commission before substantial delegated work. Use when starting a non-trivial coding, research, writing, or planning effort; when the user asks to "scope this", "write a commission", "shape the work", "make the brief", or when an agent needs authority, boundaries, outcomes, and verification before executing. Produces a commission document.
---

# Commission Work

A commission is a work brief that grants authority and context. It states outcomes, boundaries, and verification without turning into a step-by-step recipe.

Use this before substantial work, especially when the task could sprawl, touch multiple files, require research, or benefit from premise-checking.

## 1. Orient

Read the user request and any nearby project docs. Identify:

- Why this work exists
- Who or what benefits
- What is already decided
- What must not be touched
- What could make the request wrong or wasteful

If the premise seems off, record the concern inside the commission instead of silently obeying.

## 2. Choose a commission path

Use an existing project convention if one exists. Otherwise create:

```text
_meta/commissions/active/YYYY-MM-DD-short-slug.md
```

If the project has no `_meta/`, use:

```text
docs/commissions/YYYY-MM-DD-short-slug.md
```

Do not invent hidden state. The commission must live in the repo or workspace where future agents can find it.

## 3. Write the commission

Include:

- Title
- Date
- Status
- Telos: why the work exists
- Authority granted: what the runner may do without asking
- Boundaries: what not to touch or assume
- Context: facts the runner should know
- Outcomes: end states, not steps
- Verification: how each outcome will be checked
- Risks and adversarial questions
- Expected record: where the wrap-up/chronicle/report should land

## 4. Keep it outcome-shaped

Avoid:

- Exact implementation steps
- File-by-file recipes
- Tool micromanagement
- Vague "make it better" outcomes

Prefer:

- "Users can export CSV from the dashboard, proven by..."
- "The repo has a public catalog with only packaged skills..."
- "The draft is ready for critique, with open assumptions listed..."

## 5. Run or hand off

If continuing in the same session, use the commission as the north star and update it when scope changes. If handing off, make the next action explicit.

## 6. Close it

When work ends, move it to a complete folder if the project has one, and link the final record. If there is no local convention, append a `Result` section with:

- What changed
- What was verified
- What failed
- What remains
- Where follow-up is tracked
