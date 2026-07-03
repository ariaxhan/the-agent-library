---
name: reality-audit
description: >-
  Audit a "done" report or near-final artifact against reality. Use when an AI agent
  or a person reports work as finished, or when something substantial is about to be
  sent, published, submitted, or shipped. Separates corroborated structure from
  self-reported metrics, hunts real defects before release, and returns a trust or
  ship/hold verdict tied to live checks.
---

# Reality Audit

A worker cannot certify its own work. When something claims to be done, the claim and the proof often come from the same source. When something is about to ship, the maker reads what they meant, not what is there. This audit creates the separate check.

Use it on any hand-off you are about to trust or artifact you are about to send: an assistant that says it emailed the team, updated the doc, booked the trip, finished the draft, hit a number, or prepared a near-final launch artifact.

## Choose the entry mode

- **Done-report mode:** start from claims. Split what was reported from what is proven.
- **Pre-ship mode:** start from the artifact. Assume it is broken and look for what would embarrass, mislead, or get rejected.

## 1. Split the claims into two piles

For done-report mode, read the report and sort every claim:

- **Structural**, something exists or ran: a file was created, a message was sent, a step executed, a section was added, a setting was changed.
- **Self-reported metric**, a number or judgment the worker assigned itself: "100% done", "all checks pass", a score, a quality rating, "fully tested".

The two piles get checked differently. Most false confidence hides in the second pile dressed up as the first.

## 2. Corroborate the structural claims yourself

For each structural claim, look at the actual artifact, not the summary of it:

- "Sent the email" → open the sent folder and read it.
- "Updated the doc" → open the doc and find the change.
- "Added the section" → read the section.

Never accept the worker's description of its own output as proof the output exists. If you cannot find the artifact, the claim is unconfirmed, full stop.

## 3. Attack what "complete" hides

For pre-ship mode, review as if you have never seen the work and someone told you it is broken. Hunt defects that survive a confident "done":

- wrong language, locale, currency, audience, date, name, or link
- an error swallowed as success
- a claim that does not match the actual artifact
- a path nobody walked end-to-end

Split findings into **real defects** (would embarrass, mislead, or get rejected) and **out-of-scope / nitpicks**. Rank real defects first.

## 4. Root-cause the class, not the instance

For each real defect, ask whether it is one-off or a symptom. One stale link usually means others; one wrong locale often means more. Sweep siblings before shipping.

## 5. Do not launder metrics into facts

For every self-reported metric you cannot re-run right now:

- Mark it **plausible but unverified**, never copy it forward as established truth.
- Attach an explicit re-check hook: the exact thing a later checker should do ("to confirm, re-run the report and read row 4", "open the live page and complete the signup yourself").

A metric you carry forward unmarked becomes a "fact" nobody ever actually checked. That is where wasted rounds come from.

## 6. Separate leverage from spectacle

Some claims impress by volume ("processed 4,000 items", "ran 50 checks") without proving the thing works. Flag scale-as-spectacle separately from evidence. Big numbers are not corroboration; a single exercised end-to-end path is.

## 7. Issue the verdict

State plainly, per claim cluster:

- **Believe the structure**: corroborated against the real artifact.
- **Provisionally trust the metrics**: self-reported, re-check hooks attached.
- **Ship / hold**: tied to the specific live re-check you performed.

Carry the principle through every verdict: committed is not done, done is not working. If something genuinely cannot be confirmed without a human or on-device action, say **"done: your check"**, never "it works."

## Output

Return:

- A corroboration table: claim | how it was checked | result (confirmed / unconfirmed / not found).
- A list of unverified metrics, each with its re-check instruction.
- A ranked defect list when auditing an artifact, tagged real defect or out-of-scope.
- Root-cause class for each real defect, and whether sibling cases were swept.
- A trust verdict or ship / hold verdict separating believe-the-structure from provisionally-trust-the-metrics.
- Anything you could not check, named as such, not smoothed over.
