# ground-truth

**Skills for AI work that earns trust and compounds.**

A library of copy-paste [Claude Code skills](https://code.claude.com/docs/en/skills) distilled from a few years of shipping real systems — apps, ML models, content engines, autonomous agents. Each one is a single `SKILL.md` file you can grab, drop in, and use. No framework, no install ceremony, no lock-in.

---

## The through-line

These skills come from wildly different domains — shipping iOS apps, training taste models, running daily content pipelines, orchestrating fleets of coding agents. But they're all the same move underneath: **make the AI earn trust instead of claiming it, and make the work compound instead of starting from zero.**

Four pillars run through everything here:

1. **Externalized judgment that compounds.** Memory, decisions, and hard-won lessons live in durable, version-controlled files — so the next session (or the next person) inherits them instead of relearning. → `agent-tradition`, `train-a-taste-model`
2. **Earned confidence.** Nothing is "good" because it sounds good. Prove it beats the cheap baseline — verify live, score against the crowd, residualize the confound, let a blind grader judge. → `verify-live-not-committed`, `research-failures-first`
3. **Mechanical enforcement over good intentions.** If a rule must hold, a hook enforces it. Prose rules get ignored ~40% of the time under load; hooks approach zero. → `rules-need-hooks-not-prose`, `runaway-agent-killswitch`
4. **Operate fuzzy work as systems.** Writing, research, content, shipping — turned into staged pipelines with provenance, gates, and feedback loops instead of vibes. → `humanize-ai-prose`, `ship-ios-to-testflight-keyonly`

---

## How to use these

**Grab one skill (the intended way):**

Every skill is one self-contained file. Copy the `SKILL.md` you want into your skills folder:

```bash
# personal (all your projects)
mkdir -p ~/.claude/skills/ship-ios-to-testflight-keyonly
curl -o ~/.claude/skills/ship-ios-to-testflight-keyonly/SKILL.md \
  https://raw.githubusercontent.com/ariaxhan/ground-truth/main/skills/ship-ios-to-testflight-keyonly/SKILL.md

# or project-scoped: drop it in <your-repo>/.claude/skills/
```

That's it. Claude picks it up automatically when relevant, or you invoke it with `/ship-ios-to-testflight-keyonly`. Some skills ship a companion file (a `Fastfile.example`, a `reference.md`, a `killswitch.sh.example`) — grab the folder if you want those too.

**Or add the whole library as a marketplace:**

```
/plugin marketplace add ariaxhan/ground-truth
/plugin install ground-truth@ground-truth
```

One command, all the skills, auto-updates when new ones land. But copy-paste always works — take only what you need.

---

## The catalog

8 skills are shipped and polished today; the rest are mapped and rolling out. Full list with one-liners and status: **[CATALOG.md](./CATALOG.md)**.

**Shipped now:**

| Skill | What it does |
|---|---|
| [`ship-ios-to-testflight-keyonly`](./skills/ship-ios-to-testflight-keyonly) | Build & upload iOS + macOS to TestFlight with only an App Store Connect API key — zero manual clicking |
| [`agent-tradition`](./skills/agent-tradition) | Give AI agents durable institutional memory + hook-enforced session accountability that compounds |
| [`research-failures-first`](./skills/research-failures-first) | Research real-world failure modes before building — a symptom→cause→fix→URL map from post-mortems |
| [`verify-live-not-committed`](./skills/verify-live-not-committed) | Make an agent prove a change works against the live system before calling it done |
| [`rules-need-hooks-not-prose`](./skills/rules-need-hooks-not-prose) | Enforce critical agent rules with hooks it can't bypass, not prose it ignores |
| [`runaway-agent-killswitch`](./skills/runaway-agent-killswitch) | Stop a looping autonomous agent from burning budget overnight (fail-open, PreToolUse) |
| [`humanize-ai-prose`](./skills/humanize-ai-prose) | Rewrite AI text into genuinely human prose with seven ordered transform passes |
| [`train-a-taste-model`](./skills/train-a-taste-model) | Train a small model on your own archive that ranks new items the way you would |

---

## Provenance

Every skill here was extracted from a system that actually shipped and a lesson that was actually paid for — not invented for a blog post. Where a skill encodes a number (a 78% find-rate, a 40% violation rate, a confidence threshold), that number came from real runs. Where it warns about a trap, something fell in the trap first.

Distilled from real work by [Aria Han](https://github.com/ariaxhan). MIT licensed — take it, change it, ship it.
