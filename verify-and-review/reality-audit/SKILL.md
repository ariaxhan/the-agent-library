---
name: reality-audit
description: Grade a "done" report against what is actually true. Use when an AI agent or a person reports work as finished ("done", "I built it", "all checks pass", "here are the results") and you need to separate what is corroborated from what is only self-reported. Triggers include "did it really do what it says", "verify this done report", "grade the agent's results", "is this actually finished". Produces a corroboration table, a list of unverified claims with re-check instructions, and a trust verdict.
---

# Reality Audit

A worker cannot be skeptical of its own report. When something claims to be done, the claim and the proof are coming from the same source, so a separate audit is the only thing that turns "it says it works" into "it works." This is that audit.

Use it on any hand-off you are about to trust: an assistant that says it emailed the team, updated the doc, booked the trip, finished the draft, or hit a number.

## 1. Split the claims into two piles

Read the report and sort every claim:

- **Structural**, something exists or ran: a file was created, a message was sent, a step executed, a section was added, a setting was changed.
- **Self-reported metric**, a number or judgment the worker assigned itself: "100% done", "all checks pass", a score, a quality rating, "fully tested".

The two piles get checked differently. Most false confidence hides in the second pile dressed up as the first.

## 2. Corroborate the structural claims yourself

For each structural claim, look at the actual artifact, not the summary of it:

- "Sent the email" → open the sent folder and read it.
- "Updated the doc" → open the doc and find the change.
- "Added the section" → read the section.

Never accept the worker's description of its own output as proof the output exists. If you cannot find the artifact, the claim is unconfirmed, full stop.

## 3. Do not launder metrics into facts

For every self-reported metric you cannot re-run right now:

- Mark it **plausible but unverified**, never copy it forward as established truth.
- Attach an explicit re-check hook: the exact thing a later checker should do ("to confirm, re-run the report and read row 4", "open the live page and complete the signup yourself").

A metric you carry forward unmarked becomes a "fact" nobody ever actually checked. That is where wasted rounds come from.

## 4. Separate leverage from spectacle

Some claims impress by volume ("processed 4,000 items", "ran 50 checks") without proving the thing works. Flag scale-as-spectacle separately from evidence. Big numbers are not corroboration; a single exercised end-to-end path is.

## 5. Issue the verdict

State plainly, per claim cluster:

- **Believe the structure**: corroborated against the real artifact.
- **Provisionally trust the metrics**: self-reported, re-check hooks attached.

Carry the principle through every verdict: committed is not done, done is not working. If something genuinely cannot be confirmed without a human or on-device action, say **"done: your check"**, never "it works."

## Output

Return:

- A corroboration table: claim | how it was checked | result (confirmed / unconfirmed / not found).
- A list of unverified metrics, each with its re-check instruction.
- A trust verdict separating believe-the-structure from provisionally-trust-the-metrics.
- Anything you could not check, named as such, not smoothed over.
