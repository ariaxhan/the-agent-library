---
name: fresh-eyes-adversary-pass
description: Run a fresh, adversarial review on near-final work before it ships. Use when something substantial is finished and about to be sent, published, or submitted — a deck, a contract, a launch email, a research report, a product page, an application. Triggers include "find what's broken before I send this", "fresh eyes on this", "review before launch", "assume it's broken and attack it", "what would a reviewer reject". Produces a ranked defect list separating real defects from nitpicks, with a ship-or-hold verdict tied to a live re-check.
---

# Fresh-Eyes Adversary Pass

The person who made the thing cannot be the one who certifies it — they read what they meant, not what's there. This is the opposite stance: come in cold, assume it's broken, and try to break it before a reviewer, a customer, or reality does.

Run it on anything substantial right before it leaves your hands.

## 1. Reset to a cold, hostile stance

Review as if you have never seen this work and you've just been told it's broken. Separate the maker from the auditor for real — a fresh chat, a different session, or a deliberate dump of every assumption you carried in. A maker auditing their own numbers will pass them; that's the failure mode this exists to defeat.

## 2. Attack what "complete" hides

Hunt the defects that survive a confident "done":

- Wrong language, locale, currency, or audience slipped through.
- An error that was swallowed and looks like success.
- A stale value — an old price, name, date, or link copied from a previous version.
- A claim in the work that does not match the actual artifact.
- The one path nobody actually walked end-to-end.

Go look at the live artifact, not the summary of it.

## 3. Sort findings: real vs out-of-scope

Split everything you found into **real defects** (would embarrass, mislead, or get rejected) and **out-of-scope / nitpicks** (taste, future work). Be explicit which is which, and rank the real ones by severity. A long list of nitpicks must not bury the one blocker.

## 4. Root-cause the class, not the instance

For each real defect, ask whether it's a one-off or a symptom. One stale link usually means others; one section in the wrong language usually means more. Sweep for the siblings now. A fix that patches only the visible instance is a regression already in waiting.

## 5. Fix, then re-confirm live

Fix the real defects. Then verify against the live artifact — open the real thing and check, don't re-read the report. Ship only after the blockers are gone and confirmed in reality.

## Output

Return:

- A ranked defect list, each tagged real defect or out-of-scope, ordered by severity.
- The root-cause class for each cluster, and whether the siblings were swept.
- A ship / hold verdict, tied to a specific live re-check that was actually performed.
