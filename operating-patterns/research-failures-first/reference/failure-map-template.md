# Failure-map template

Copy this into `research/<topic>.md` in your durable notes store and fill it in. Subsequent
work cites specific row numbers from it. Aim for a **minimum ~10 unique entries** — below 10
usually means the channels weren't queried hard enough; expand the search or add the forums
channel before declaring the map done. Every row needs a resolving source URL — no URL, no row.

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
