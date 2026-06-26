---
name: extract-source-to-notes
description: Ingest one external source into structured notes. Use when the user drops a Medium article, blog post, paper, URL, transcript, or pasted text and asks to "extract this", "process this article", "distill this URL", "pull the insights from this", or capture one source with provenance. Produces raw provenance, distilled claims, contradictions, tags, and follow-up sparks.
---

# Extract Source To Notes

One source in, structured notes out. This is not a web hunt; process exactly one source unless the user asks otherwise.

## 1. Capture provenance

Create or update a note with:

- Source title
- URL or origin
- Author/publisher if known
- Publish date or access date
- Capture date
- Source type: article, paper, docs, transcript, pasted text, other

Default path:

```text
notes/sources/YYYY-MM-DD-short-slug.md
```

Use the project's existing notes folder if one exists.

## 2. Read for claims, not summary

Extract:

- Thesis
- 3-7 key claims
- Evidence for each claim
- Concrete examples, numbers, names, tools, or mechanisms
- Assumptions
- Caveats
- Contradictions or tensions
- Terms that need definitions

Do not flatten the source into generic "key takeaways."

## 3. Write the distilled note

Use:

```markdown
# <source title>

## Provenance
- Source:
- Author:
- Published:
- Captured:
- Type:

## Thesis
<one paragraph>

## Claims
1. **Claim:** ...
   **Evidence:** ...
   **Why it matters:** ...

## Contradictions / Tensions
- ...

## Useful Details
- ...

## Tags
- ...

## Follow-up Sparks
- ...
```

## 4. Check against existing notes

Search nearby notes for the topic, author, key terms, and claims. Mark:

- Reinforces existing note
- Contradicts existing note
- Adds new detail
- Replaces stale belief
- Needs follow-up

If there is no notes archive, say that collision checking was not available.

## 5. Report back

Return:

- Where the note was written
- The strongest insight
- Any contradictions found
- Follow-up questions or research leads
- Anything not captured because the source was inaccessible

## 6. Boundaries

If a URL cannot be fetched, ask for pasted text or use a clearly marked partial capture from available metadata. Never pretend you read a blocked source.
