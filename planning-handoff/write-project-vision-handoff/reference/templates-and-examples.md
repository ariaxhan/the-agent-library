# Vision Handoff — Templates & Examples

Full document templates and worked example patterns. Moved out of SKILL.md. Load when actually writing VISION.md / FLOWCHARTS.md.

## VISION.md Template

```markdown
# [PROJECT NAME] — [One-Line Description]

<!--
●CONTEXT|type:seed_document|for:coding_agent|purpose:[specific_purpose]
-->

## WHAT THIS IS

[One paragraph. What exists or should exist. No implementation details.]

## THE PROBLEM

[What friction/gap/need drove this. Be specific. Include user quotes if relevant.]

## THE SOLUTION

[High-level approach. Philosophy, not implementation. Why this approach over alternatives.]

## KEY DECISIONS

| Decision | Rationale | Alternatives Rejected |
|----------|-----------|----------------------|
| [choice] | [why] | [what else was considered] |

## DESIGN CONSTRAINTS

- [Hard limit 1]
- [Hard limit 2]
- [Non-negotiable requirement]

## ANTI-REQUIREMENTS

What this is NOT:
- ❌ [Explicit exclusion with reason]
- ❌ [Another thing to avoid]

## CONSIDERATIONS FROM PLANNING

[Critical context from the conversation that shapes implementation:]
- [Consideration 1: why it matters]
- [Consideration 2: edge case discussed]
- [Tradeoff acknowledged]

## SUCCESS CRITERIA

How to know it works:
- [ ] [Measurable outcome 1]
- [ ] [Measurable outcome 2]

## YOUR TASK

[Direct instruction to coding agent. What to do first. What to prioritize. What to critique before building.]
```

## FLOWCHARTS.md Template

```markdown
# [PROJECT NAME]: Architecture Breakdown

## 1. CORE CONCEPT

[One paragraph a teenager could understand. No jargon without immediate definition.]

## 2. GLOSSARY

| Term | Plain English Definition |
|------|-------------------------|
| [technical term] | [simple explanation] |

## 3. THE FLOW

[ASCII diagram showing information/action flow]

```
┌─────────┐     ┌─────────┐     ┌─────────┐
│ Input   │────▶│ Process │────▶│ Output  │
└─────────┘     └─────────┘     └─────────┘
```

## 4. WHAT HAPPENS WHEN [Scenario]

[Step-by-step walkthrough of a typical use case]

## 5. COMPONENT BREAKDOWN

### [Component Name]
- **Purpose**: [one sentence]
- **Receives**: [what comes in]
- **Produces**: [what goes out]

## 6. QUESTIONS TO VERIFY UNDERSTANDING

Before proceeding, can you answer:
1. [Question about core concept]
2. [Question about flow]
3. [Question about component interaction]
```

## Coding Agent Instructions block (append to end of VISION.md)

```markdown
## INSTRUCTIONS FOR CODING AGENT

1. **First**: Read both VISION.md and FLOWCHARTS.md completely
2. **Then**: Critique this architecture; identify simplifications
3. **Before building**: Confirm understanding of constraints and anti-requirements
4. **During build**: Reference KEY DECISIONS for rationale
5. **If unclear**: The considerations exist for a reason; don't discard them
```

## Example Patterns

**Good decision capture:**
```markdown
| Use SQLAlchemy ORM | User explicitly stated; team familiarity | Raw SQL (maintenance), Django ORM (overkill) |
```

**Good consideration:**
```markdown
- Session persistence: User works for minutes at a time; knowledge dies when session ends. Any solution must capture learning automatically, not require manual action.
```

**Good anti-requirement:**
```markdown
- ❌ Not a tutorial system (user is already expert; don't explain basics)
```

**Good coding agent task:**
```markdown
## YOUR TASK

1. Critique this architecture; propose simplifications
2. Build core functionality first; optional features later
3. Prioritize: learning capture → config updates → test automation
4. Report what you built and any deviations from this spec
```
