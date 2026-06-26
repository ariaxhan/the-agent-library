---
name: manage-a-knowledge-base
description: Run a personal knowledge base or second brain as a system, not a junk drawer. Use for any stage of a notes collection — "process my inbox / triage my captures", "find contradictions across my notes", "synthesize / weave these notes together", "prune / clean up my ideas list", "archive stale notes / decay scan", "check my notes for broken links or missing metadata", "manage my vault / zettelkasten / second brain". Produces filed notes, collision logs, synthesis notes, a pruned idea list, archive decisions, and an integrity report, depending on the phase invoked.
---

# Manage a Knowledge Base

A notes collection has a lifecycle. Captures come in raw, get sorted, get connected, get synthesized, and eventually decay — and the whole thing drifts into broken links and duplicates unless something maintains it. This kit is the six maintenance moves, each a self-contained workflow in `reference/`.

Pick the phase that matches what the collection needs right now. You don't run all six every time.

## The lifecycle

```
CAPTURE → TRIAGE → CONNECT → SYNTHESIZE → CURATE → DECAY
                                                    ↑
                              INTEGRITY (periodic cross-check)
```

- **Triage** — turn a pile of raw captures into filed, structured notes. → `reference/triage-captures.md`
- **Connect** — find where notes contradict, reinforce, or unexpectedly bridge. → `reference/find-collisions.md`
- **Synthesize** — knit several notes into one integrated piece aimed at a question. → `reference/synthesize-notes.md`
- **Curate** — prune the idea backlog; graduate the clusters that earned it. → `reference/curate-ideas.md`
- **Decay** — score notes by use and age; archive the cold, promote the proven. → `reference/decay-and-archive.md`
- **Integrity** — audit metadata, links, and contradictions across the whole base. → `reference/audit-integrity.md`

## Which phase do I need?

| The user says… | Phase | Reference |
|---|---|---|
| "process my inbox", "I have a pile of unsorted captures" | Triage | `reference/triage-captures.md` |
| "what contradicts what", "find connections across my notes" | Connect | `reference/find-collisions.md` |
| "synthesize these", "knit these threads", "the bigger picture" | Synthesize | `reference/synthesize-notes.md` |
| "clean up my ideas", "which ideas are worth keeping" | Curate | `reference/curate-ideas.md` |
| "archive stale notes", "my base is bloated", "decay scan" | Decay | `reference/decay-and-archive.md` |
| "broken links", "missing metadata", "integrity check" | Integrity | `reference/audit-integrity.md` |

## Principles that hold across every phase

- **Batch the judgment moments — never auto-promote.** The value of a note system is the human deciding what's worth keeping. Surface decisions in small batches; don't let the assistant silently file or delete.
- **Recurrence beats excitement.** A pattern, idea, or cluster graduates only when it shows up across multiple independent sessions — one enthusiastic capture is not a trend.
- **Confidence threshold over volume.** One strong, real finding beats ten maybes. False positives erode trust in the whole system faster than missed ones.
- **Protect the evergreen.** Anything marked durable is never auto-archived, however old or untouched.

## Output

Each phase produces its own artifact — filed notes, a dated collision log, a synthesis note, a pruned idea file, archive/promotion decisions, or an integrity report with a pass rate. Open the matching reference for the exact steps and output format.
