# Skill Methodology

Date: 2026-06-25

This repo is a category-first skill collection. Top-level category folders are shelves; each child folder with `SKILL.md` is a skill.

Default target: **general-purpose Claude usage for non-coders** — thinking, deciding, verifying, researching, writing, running work. The spine of the library is the verify-and-review family: how to trust AI work instead of believing its "done." Code skills are one category, not the center. Each code skill must be **standalone** — it works on its own, copied alone, with no dependency on a parent system, local AgentDB, hooks, private paths, or sibling skills.

Rules and one-line principles are not skills. The valuable ones are folded into the skill they support (as a short principle inside the workflow), not shipped as standalone "skills" or a separate rules pack.

## Skill Bar

A packaged skill must pass all five checks:

1. **Workflow:** at least three ordered moves, or one staged judgment process with a clear start and end.
2. **Non-obvious know-how:** sequence, traps, tradeoffs, or templates an agent would not reliably infer from the task alone.
3. **Concrete output:** writes, changes, submits, audits, or produces a named artifact.
4. **Sharp trigger:** `description:` names real user phrasings and when to use it.
5. **Portable package:** no private paths, project-only state, secrets, or unstated local helper dependencies.

## Artifact Categories

| Category | Definition | Repo home |
|---|---|---|
| Packaged skill | Meets the bar and is safe to copy into a skills directory. | The matching top-level category folder |
| Draft skill | Workflow is real, but name/body/trigger/output still need work before publishing. | Category folder with explicit draft status |
| Process engine | Standalone loop that changes how Claude approaches work across domains. | `process-engines/` |
| Candidate skill | Existing source skill that looks exportable but has not been de-branded yet. | `docs/existing-skills-audit.md` until packaged |
| Local-wrapper candidate | Real workflow, but currently depends on local helper skills, local directories, or Vaults naming. | audit doc first, package only after dependency rewrite |
| Operating-pattern skill | Meta workflow, methodology, or installable practice that still has a clear use case. | `operating-patterns/` |
| Reject | Too generic, too local, or not a workflow. | do not catalog |
| Reject | Too generic, too local, or not a workflow. | do not catalog |

## Review Procedure

For each existing source skill:

1. Read `SKILL.md` and any directly referenced files needed to understand the workflow.
2. Identify the user-facing trigger phrases from the frontmatter.
3. Name the concrete output.
4. Mark hidden dependencies: local folders, helper skills, network requirements, commands, or private conventions.
5. Categorize using the table above.
6. Decide the export move: copy as-is, de-brand, split, merge with another skill, demote, or reject.
7. For code-related candidates, check `kernel-claude` first and generalize the strongest existing workflow instead of inventing from scratch.

## Category Standards

**Packaged skill:** can be copied today and still work for a stranger.

**Draft skill:** belongs in its category folder only if the intended workflow is clear and the draft warning is explicit.

**Candidate skill:** promising, but not copied yet. This avoids making the repo look more done than it is.

**Local-wrapper candidate:** useful, but only after replacing local helper calls with bundled instructions or explicit companion skills.

**Operating-pattern skill:** may be broader than a workflow skill, but it still needs a trigger, an action path, and a concrete use. Avoid preserving vague principles with no operation.

**Code-engineering skill:** must be portable. Remove or soften local-only assumptions such as AgentDB, exact hook names, private paths, or project-specific branch rules. Keep the useful method.
