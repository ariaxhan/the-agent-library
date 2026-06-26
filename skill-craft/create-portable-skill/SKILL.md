---
name: create-portable-skill
description: Create, audit, or package a portable Claude/Codex skill. Use when building a new skill, converting an existing workflow into a reusable skill, reviewing whether something is a real skill or just a rule/reference/kit, or preparing a skills repository catalog.
---

# Create Portable Skill

Create skills that another agent can actually use. A skill is a packaged workflow, not a rule, essay, prompt dump, or product pitch.

## 1. Classify the candidate

Before writing files, decide what the artifact is:

| Type | Definition | Destination |
|---|---|---|
| Packaged skill | Multi-step workflow, concrete output, portable dependencies | `skills/<name>/` |
| Draft skill | Real workflow but incomplete body, name, trigger, or bundled files | `skills/<name>/` with explicit draft status |
| Kit | Installable system made of hooks, templates, multiple files, or multiple skills | `kits/` |
| Rule/pattern | Principle, invariant, hook pattern, or one-step guardrail | `rules/` or docs, not `skills/` |
| Reference | Background methodology a skill can point to | `references/` |
| Reject | Too vague, too local, not a workflow, no crisp trigger | Do not catalog |

If it could be one bullet in a rules file, do not make it a skill.

## 2. Apply the skill bar

A packaged skill must pass all five:

1. **Workflow:** at least three ordered moves, or one staged judgment process with a clear start and end.
2. **Non-obvious know-how:** sequence, traps, tradeoffs, or templates an agent would not reliably infer.
3. **Concrete output:** writes, changes, submits, audits, or produces a named artifact.
4. **Sharp trigger:** `description:` names real user phrasings and when to use it.
5. **Portable package:** no private paths, secrets, project-only state, or hidden local helper dependencies.

## 3. Name it plainly

Use lowercase hyphen-case. Prefer verb-led names that say the output:

- Good: `write-project-vision-handoff`, `critique-vision-handoff`, `hunt-research-sources`
- Bad: clever names, metaphors, acronyms, or one-word vibes

Folder name and frontmatter `name:` must match exactly.

## 4. Write the trigger first

The frontmatter `description:` is the discovery surface. It must include:

- What the skill does
- When to use it
- Real user phrasings when possible
- The concrete output

Use third person and be specific. The body loads only after the skill triggers, so do not hide trigger logic in the body.

## 5. Package the folder

Minimum:

```text
skills/<name>/
  SKILL.md
  agents/openai.yaml
```

Add bundled files only when they directly support execution:

- `reference/` for templates, output formats, checklists, or long examples
- `scripts/` for deterministic repeatable operations
- `assets/` for templates or media used in outputs

Do not add README, changelog, installation guide, or extra docs inside the skill folder.

## 6. Validate

Check:

- `SKILL.md` starts with YAML frontmatter.
- Frontmatter has only `name:` and `description:`.
- `name:` matches folder.
- Referenced files exist.
- Private names, absolute user paths, secrets, and project-only assumptions are removed.
- `agents/openai.yaml` has a short display name, short description, default prompt, and invocation policy.

## 7. Update the catalog

Add the skill to exactly one primary category. If it is draft, local-wrapper, kit, rule, reference, or reject, say that honestly. The catalog is a shelf, not a dream board.
