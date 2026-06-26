---
name: research-failures-first
description: Before building anything non-trivial, research real-world failure modes from production post-mortems and issue trackers and produce a committed symptom→cause→fix→URL map — instead of donating your own debugging time or asking the model to hallucinate what could break.
---

# Research Failures First

## What this is

A protocol that inverts the default workflow. Instead of searching for the happy path
("how to use X") and discovering its sharp edges by stepping on them, you hunt for
**other people's already-debugged pain first** and turn it into a committed reference: a
symptom → root-cause → fix → source-URL table for the specific thing you're about to
build. Most non-trivial implementation pain is somebody else's solved problem. Finding
their bruises before donating your own runs about **5× return** on the time spent looking.

## Why it beats the default

The default happy-path search optimizes for "make it work once" and hides every failure at
the boundaries — empty input, the second concurrent writer, the migration that runs twice,
the auth token that expires mid-request. Those are exactly what people who hit production
already documented. You want their post-mortems, not a tutorial.

## When it gates implementation

Mandatory **before** writing code for:

- **Native dependency adoption** — any new package (npm/pip/cargo/brew/gem/go) not already in the repo.
- **Schema migrations** — DB or content, especially anything backfilling or irreversible.
- **Auth flow changes** — login, tokens, sessions, OAuth, permissions.
- **Sync protocol work** — OTA, websockets, event sourcing, conflict resolution.
- **Store / marketplace submission gates** — App Store, Play Store, extension marketplaces.
- **Cross-cutting refactors** — more than ~5 files, or multi-module.
- **Framework upgrades** that change the public API surface.

NOT required for: typo and copy fixes, comment changes, single-file bug fixes inside
familiar code, or test additions to an existing suite.

## The channel ranking

Empirically ranked by **unique-find rate** — how often a channel surfaces a failure no
other channel did (from a controlled run of parallel research agents, each locked to one
channel on identical topics):

| Channel | What it is | Unique-find rate | Run? |
|---|---|---|---|
| Production case studies — engineering-blog post-mortems, incident write-ups | 78% | **always** |
| Issue tracker — the project's OWN GitHub/GitLab issues, open + closed | 47% | **always** |
| Forums — Reddit, Hacker News, Stack Overflow | 29% | optional supplement, if the issue tracker returns < ~20 entries |
| Generic web search — "X gotchas", "X common mistakes" | 15% | **never — drop it** |

**Rule:** always run the top two **in parallel**. The generic "gotchas" search mostly
re-derives the issue tracker at lower quality — it's a waste of a slot. Use forums only to
top up a thin result set.

## The deliverable

One persistent, committed file at `research/<topic>.md` in your durable notes store.
Subsequent work cites specific row numbers from it. Format:

```markdown
---
topic: <topic name>
status: canonical
last_updated: YYYY-MM-DD
channels_run: [post-mortems, issue-tracker]
entries: <count>
---

# <Topic> failure modes

## TL;DR
1–3 sentences: what works, what to avoid, the stack verdict.

## Failure-mode table
| # | Symptom | Root cause | Fix | Source URL |
|---|---|---|---|---|
| 1 | <what the user/operator sees> | <why it breaks> | <minimal fix> | <link> |
| 2 | ... | ... | ... | ... |

## Pre-flight checklist
- [ ] <item from the table to verify before this work starts>
- [ ] ...

## Notes
Open questions, version-specific caveats.
```

**Minimum ~10 unique entries.** Below 10 usually means the channels weren't queried hard
enough — expand the search or add the forums channel before declaring the map done.

## The hard rule: cite sources, never hallucinate failures

**Never ask the model what could go wrong.** Foundation models confidently invent failure
modes that don't exist for your specific version, and omit the real ones. **Every row needs
a resolving source URL** — a real post-mortem, issue, or thread you can open. No URL, no
row. The map is only as trustworthy as its weakest citation.

## Optional parallel orchestration

When you have sub-agents, run it as a sprint and keep raw research out of the orchestrator's
context:

1. **Pre-log a PENDING row** per channel before spawning, so a dropped agent is visible.
2. **Spawn the two top channels in parallel** (single dispatch, isolated worktrees if you
   have them). Each writes to `research/<topic>-channel-<name>.md`.
3. **Cap each return summary** at a couple hundred words — the deliverable is on disk.
4. **Verify by file, not by receipt.** Open the file the agent claims it wrote. Missing
   file or still-PENDING row → re-spawn that one channel (max one retry).
5. **Merge** both files into canonical `research/<topic>.md`. Dedupe overlapping rows,
   citing both source URLs in the merged entry.

## Anti-patterns

- **Skipping research because "this is quick."** The cheap-research → expensive-rebuild loop is exactly what this kills (~5× ROI).
- **Asking the model what breaks** instead of searching. Hallucinated, version-wrong, no URL.
- **Running the generic "gotchas" search alone.** 15% unique — spend the time on the top two.
- **Treating the map as ephemeral.** It's committed reference; later work cites its rows.
- **Letting a receipt stand in for a file.** No map on disk = the protocol didn't run.
