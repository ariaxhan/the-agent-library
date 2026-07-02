# the-agent-library

**A curated library of portable skills for getting real work out of AI agents.** Built for Claude, Codex, and any agent that loads skills. Most of them are not about code at all.

This repo *is* the collection. There is no single `skills/` drawer. Each top-level folder is a category shelf, and every child folder with a `SKILL.md` is one skill you can copy and use on its own.

## The through-line

Strip away the domain and the same move runs through almost everything here: **make AI work you can actually trust, instead of believing it when it says "done."** The strongest skills are judgment processes. Audit the claim, test the measuring stick, question the premise, get fresh eyes. They matter whether you are writing, researching, planning, or shipping, and you do not need to be a coder to need them. [`verify-and-review/`](./verify-and-review) is the spine of the library.

## What a skill is

Every skill is a self-contained folder:

```text
<skill-name>/
  SKILL.md            the workflow itself: a trigger plus ordered steps
  agents/openai.yaml  display name, short description, default prompt
  reference/          optional: templates, checklists, or long examples
```

A skill earns its place only if it is a real workflow (multi-step, non-obvious know-how, a sharp trigger, a concrete output), not a one-line rule dressed up as a skill.

## Repo layout

| Folder | Skills | What lives here |
|---|---|---|
| [`verify-and-review/`](./verify-and-review) | 4 | Trusting AI work: audits, premise checks, adversarial review |
| [`process-engines/`](./process-engines) | 6 | Forge, dream, brainstorm, experiment, debate, and speech loops for better thinking |
| [`planning-handoff/`](./planning-handoff) | 2 | Specs, handoffs, critiques, implementation readiness |
| [`work-management/`](./work-management) | 4 | Commissions, chronicles, learning synthesis, bounded autonomous loops |
| [`research-notes/`](./research-notes) | 3 | Source hunts, single-source extraction, a full knowledge-base kit |
| [`creative-taste/`](./creative-taste) | 2 | Writing, voice, and personal taste models |
| [`skill-craft/`](./skill-craft) | 1 | Creating, auditing, and packaging skills |
| [`code-engineering/`](./code-engineering) | 8 | Standalone coding workflows (one category, not the point) |
| [`shipping/`](./shipping) | 3 | Release and launch workflows |
| [`operating-patterns/`](./operating-patterns) | 3 | Meta and methodology-shaped skills |

36 skills total. [`docs/`](./docs) holds audits and maintenance notes, not installable skills.

## The full shelf

See [CATALOG.md](./CATALOG.md) for every skill, grouped by category, each with the exact trigger that should fire it. That file is the source of truth for what exists; this README stays short on purpose.

## What makes the cut

- **General-purpose first.** A skill should help a stranger get more out of an agent, not just fit one private setup.
- **A workflow, not a rule.** Multi-step, non-obvious know-how, a sharp `Use when` trigger, and a concrete output. One-line principles get folded into the skill they support instead of shipping as fake skills.
- **Portable.** No private paths, secrets, project-only state, or hidden local dependencies. Anything a skill needs (templates, references) ships inside its folder.
- **Standalone.** Each skill, coding ones included, works on its own. Copy the one you need.
- **Literal names.** A cold reader should know what a skill does from its name alone.

## Install one skill

Copy a category child folder into your personal or project skill directory:

```bash
mkdir -p ~/.claude/skills/reality-audit
cp -R verify-and-review/reality-audit/* ~/.claude/skills/reality-audit/
```

Marketplace and plugin install is intentionally deferred until the public repo name and layout are final.

## Provenance

Distilled from real workflows by [Aria Han](https://github.com/ariaxhan). MIT licensed.
