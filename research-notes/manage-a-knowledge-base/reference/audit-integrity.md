# Audit Integrity

Periodically check the whole knowledge base for the rot that accumulates silently: missing metadata, broken links, and notes that contradict your settled conclusions.

## Steps

1. **Walk every note** (skip the archive).
2. **Check metadata** against the required-field contract for the collection: is each note tagged, dated, typed as the system expects?
3. **Verify every link and reference resolves**: internal wikilinks, cross-note references, external URLs.
4. **Flag drift**: inline tags or ad-hoc conventions that diverge from the standard.
5. **Scan for contradictions** against the durable-learnings file: notes that assert something the settled record disagrees with.
6. **Write a sectioned report** and emit a pass rate.

## Non-obvious know-how

- **Tier the findings by severity, or the report is noise:**
  - **Critical**: missing required metadata that blocks downstream automation.
  - **Warning**: convention drift that will compound if ignored.
  - **Info**: broken links, which are often intentional mid-draft and shouldn't block anything.
- A flat list of every broken link buries the one note that's silently contradicting your conclusions. Severity is what makes the audit actionable.

## Output

A dated integrity report grouped by severity (missing-metadata / invalid / broken-links / contradictions) plus an overall pass rate.
