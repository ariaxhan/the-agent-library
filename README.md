# portable-claude-skills

**A curated library of portable skills for general Claude usage.**

This repo is the skill collection. There is no single `skills/` drawer; top-level category folders are the shelves, and each child folder with a `SKILL.md` is a skill.

The default audience is general Claude usage: planning, research, writing, work management, creative systems, and AI-assisted work. Code skills exist too, but they live in [`code-engineering/`](./code-engineering) and are generalized from `kernel-claude` so they work outside Aria's local setup.

## Repo Layout

| Folder | Kind of skills |
|---|---|
| [`skill-craft/`](./skill-craft) | Skills for creating, auditing, and packaging skills |
| [`process-engines/`](./process-engines) | Forge, dream, and experiment loops for making Claude work better |
| [`planning-handoff/`](./planning-handoff) | Specs, handoffs, critiques, implementation readiness |
| [`work-management/`](./work-management) | Commissions, chronicles, bounded autonomous loops |
| [`research-notes/`](./research-notes) | Source hunts, single-source extraction, note workflows |
| [`creative-taste/`](./creative-taste) | Writing, taste models, tiny computational pieces |
| [`code-engineering/`](./code-engineering) | Portable coding workflows extracted from `kernel-claude` |
| [`shipping/`](./shipping) | Release workflows |
| [`operating-patterns/`](./operating-patterns) | Meta/operating skills and methodology-shaped skills |
| [`docs/`](./docs) | Audits and repo maintenance notes, not installable skills |

## Current Shelf

See [CATALOG.md](./CATALOG.md) for the full categorized list.

Packaged now:

- Skill craft: `create-portable-skill`
- Process engines: `forge-autonomous-work`, `dream-solution-space`, `experiment-on-rules`
- Planning/handoff: `write-project-vision-handoff`, `critique-vision-handoff`
- Work management: `commission-work`, `write-session-chronicle`, `run-autonomous-dev-loop`
- Research/notes: `hunt-research-sources`, `extract-source-to-notes`
- Creative/taste: `humanize-ai-prose`, `train-a-taste-model`
- Code engineering: `debug-code-systematically`, `refactor-code-safely`, `review-ai-code-quality`, `design-api-contracts`, `secure-code-changes`, `orchestrate-coding-agents`
- Operating patterns: `agent-tradition`, `research-failures-first`, `harden-rules-into-hooks`

Draft:

- Shipping: `build-and-release-ios-app`

## Requirements

- General-purpose first. A skill should be useful to a stranger using Claude, not only to this Vaults setup.
- Code-related skills should be extracted from `kernel-claude` when possible, then de-branded and generalized.
- No hidden local dependencies: if a workflow needs templates, references, scripts, or conventions, bundle or explain them.
- Category matters. Place each skill by the kind of work it helps Claude do, not by source repo.
- Keep names literal. A cold reader should know what the skill does.

## Install One Skill

Copy a category child folder into your personal or project skill directory:

```bash
mkdir -p ~/.claude/skills/write-project-vision-handoff
cp -R planning-handoff/write-project-vision-handoff/* ~/.claude/skills/write-project-vision-handoff/
```

Marketplace/plugin install is intentionally deferred until the public repo name and category layout are final.

## Provenance

Distilled from real workflows by [Aria Han](https://github.com/ariaxhan). MIT licensed.
