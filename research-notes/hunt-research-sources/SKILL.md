---
name: hunt-research-sources
description: Run a wide research source hunt and return a ranked findings report. Use when the user asks to "hunt for sources", "go find sources on X", "scan the web for", "do a research sweep", "find the best sources", or compare many sources before deciding what matters. Produces a sourced report with accepted findings, rejected sources, conflicts, and gaps.
---

# Hunt Research Sources

Go wide, kill noise, and bring back only findings that survive quality and novelty filters.

Use this for breadth. If the user gives one article or one URL, use a single-source extraction workflow instead.

## 1. Define the hunt

Clarify in your own notes:

- Topic
- Time sensitivity
- Source types worth prioritizing
- What counts as useful evidence
- Output path

Default output:

```text
research/YYYY-MM-DD-hunt-topic.md
```

If the project already has a research folder, use that.

## 2. Reconnaissance

Gather 8-15 candidate sources from relevant channels:

- Official docs or primary sources
- GitHub repos/issues/discussions
- Engineering blogs or postmortems
- Papers or technical reports
- Forums only when lived experience matters
- News only when the topic is current

Record source title, URL, date, and why it might matter.

## 3. Triage hard

Reject weak sources before deep reading:

- Marketing fluff
- Rewritten listicles
- Outdated material for fast-moving topics
- Paywalled/unreadable pages unless the user can provide them
- Sources that only repeat already-known claims
- Claims with no implementation detail, evidence, or examples

Aim to reject at least half.

## 4. Extract survivors

For each surviving source, capture:

- Main claim
- Concrete details: flags, numbers, configs, commands, caveats, examples
- Failure modes or tradeoffs
- Evidence strength
- What is new relative to the rest of the hunt

Avoid long quotes. Link everything.

## 5. Synthesize

Write the report:

```markdown
# Hunt: <topic> | <date>

## Summary
<5-8 bullets max>

## Top Findings
### 1. <finding>
Source: <url>
Why it matters:
Evidence:
Confidence:

## Conflicts
| Claim A | Claim B | Current read |

## Rejected Sources
| Source | Reason |

## Gaps
<What still lacks strong evidence>

## Recommended Next Moves
<What to read/build/verify next>
```

## 6. Quality gate

Before finishing:

- Every major claim has a URL.
- Findings are ranked, not dumped.
- Rejections are logged.
- Conflicts are explicit.
- Gaps are named.
- The report says what decision it supports.
