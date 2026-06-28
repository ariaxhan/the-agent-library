# the-agent-library

**A curated library of portable skills for getting real work out of AI agents — Claude, Codex, and friends — most of them not about code at all.**

This repo *is* the collection. There's no single `skills/` drawer; the top-level folders are category shelves, and every child folder with a `SKILL.md` is one skill you can copy and use.

## The through-line

Strip away the domain and the same move runs through almost everything here: **make AI work you can actually trust, instead of believing it when it says "done."** The strongest skills are judgment processes — audit the claim, test the measuring stick, question the premise, get fresh eyes — and they matter whether you're writing, researching, planning, or shipping. You don't need to be a coder to need them. [`verify-and-review/`](./verify-and-review) is the spine of the library.

## Repo Layout

| Folder | Kind of skills |
|---|---|
| [`verify-and-review/`](./verify-and-review) | Trusting AI work: audits, premise checks, adversarial review |
| [`process-engines/`](./process-engines) | Forge, dream, brainstorm, and experiment loops for better thinking |
| [`planning-handoff/`](./planning-handoff) | Specs, handoffs, critiques, implementation readiness |
| [`work-management/`](./work-management) | Commissions, chronicles, learning synthesis, bounded autonomous loops |
| [`research-notes/`](./research-notes) | Source hunts, single-source extraction, and a full knowledge-base kit |
| [`creative-taste/`](./creative-taste) | Writing and voice |
| [`skill-craft/`](./skill-craft) | Creating, auditing, and packaging skills |
| [`code-engineering/`](./code-engineering) | Standalone coding workflows (one category, not the point) |
| [`shipping/`](./shipping) | Release workflows |
| [`operating-patterns/`](./operating-patterns) | Meta/operating skills and methodology-shaped skills |
| [`docs/`](./docs) | Audits and maintenance notes, not installable skills |

## Current Shelf

See [CATALOG.md](./CATALOG.md) for the full categorized list with triggers. Highlights:

- **Verify & review:** `reality-audit`, `test-the-measuring-stick`, `audit-the-premise`, `fresh-eyes-adversary-pass`
- **Process engines:** `forge-autonomous-work`, `dream-solution-space`, `brainstorm-with-entropy`, `experiment-on-rules`
- **Work management:** `commission-work`, `write-session-chronicle`, `synthesize-learnings`, `run-autonomous-dev-loop`
- **Research & notes:** `hunt-research-sources`, `extract-source-to-notes`, `manage-a-knowledge-base` (6-phase kit)
- **Planning/handoff:** `write-project-vision-handoff`, `critique-vision-handoff`
- **Creative/taste:** `humanize-ai-prose` · **Skill craft:** `create-portable-skill`
- **Code engineering (standalone):** `debug-code-systematically`, `refactor-code-safely`, `review-ai-code-quality`, `design-api-contracts`, `secure-code-changes`, `orchestrate-coding-agents`
- **Operating patterns:** `agent-tradition`, `research-failures-first`, `harden-rules-into-hooks`
- **Draft:** `build-and-release-ios-app`

## What makes the cut

- **General-purpose first.** A skill should help a stranger get more out of Claude, not just fit one private setup.
- **A skill is a workflow, not a rule.** Multi-step, non-obvious know-how, a sharp `Use when` trigger, and a concrete output. One-line principles get folded into the skill they support — they don't ship as fake skills.
- **Portable.** No private paths, secrets, project-only state, or hidden local dependencies. If a workflow needs templates or references, they're bundled.
- **Standalone.** Each skill (coding ones included) works on its own. Copy the one you need.
- **Literal names.** A cold reader should know what a skill does from its name.

## Install One Skill

Copy a category child folder into your personal or project skill directory:

```bash
mkdir -p ~/.claude/skills/reality-audit
cp -R verify-and-review/reality-audit/* ~/.claude/skills/reality-audit/
```

Marketplace/plugin install is intentionally deferred until the public repo name and layout are final.

## Provenance

Distilled from real workflows by [Aria Han](https://github.com/ariaxhan). MIT licensed.
