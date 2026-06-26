# Vision Critique — Output Format, Techniques & Protocol

Detail moved out of SKILL.md. Load when producing the critique document.

## Output Format

```markdown
# VISION CRITIQUE: [Document Name]

## SEVERITY SUMMARY

| Level | Count | Verdict |
|-------|-------|---------|
| 🔴 BLOCKER | X | Cannot proceed until fixed |
| 🟠 MAJOR | X | Will cause implementation pain |
| 🟡 MINOR | X | Polish issues; fix if time allows |
| ⚪ NITPICK | X | Stylistic; ignore if busy |

**Overall**: [READY / NEEDS WORK / REWRITE REQUIRED]

---

## 🔴 BLOCKERS

### [B1] [Short title]

**Location**: [Section/line reference]

**Problem**: [Specific issue]

**Why it matters**: [Consequence if not fixed]

**Fix**: [Concrete action]

---

## 🟠 MAJOR ISSUES

### [M1] [Short title]
...

---

## 🟡 MINOR ISSUES

### [m1] [Short title]
...

---

## WHAT'S GOOD

[2-3 specific strengths; not empty praise]

---

## SIMPLIFICATION OPPORTUNITIES

[Things that could be removed/merged/deferred without losing core value]

---

## QUESTIONS THE CODING AGENT WILL ASK

1. [Question the spec doesn't answer]
2. [Another gap]
3. ...

[These become TODO items for the author]

---

## RECOMMENDED NEXT STEPS

1. [First fix]
2. [Second fix]
3. [Optional improvements]
```

## Critique Techniques

### The Naive Robot Test
Read the document as a literal-minded coding agent with zero context. Every place you "fill in" missing information is a spec gap.

### The Adversarial User Test
How could someone misuse, overload, or break the system as specified? If the spec doesn't address it, flag it.

### The Time Travel Test
Read the document as if you're debugging a production incident 6 months from now. What context is missing? What decisions will seem arbitrary?

### The Subtraction Test
For each component/feature: "If we removed this, would we still solve the core problem?" If yes, it's optional scope.

### The "Why" Ladder
For each decision, ask "why" three times. If you can't answer from the document alone, the rationale is missing.

### The Contradiction Hunt
Look for places where Section A implies X but Section B implies not-X. Common in long documents or multi-session planning.

## Anti-Patterns to Flag

| Pattern | Example | Problem |
|---------|---------|---------|
| **Spec as wish list** | "Should be fast, secure, scalable, easy to use" | No tradeoffs; no priorities |
| **Implementation leaking** | "Use React with Redux and..." | Over-constraining; wrong layer |
| **Passive voice decisions** | "It was decided that..." | Who decided? Why? When? |
| **Circular definitions** | "The system processes data to produce processed data" | Says nothing |
| **Feature graveyard** | Long lists with no priority | Everything gets half-built |
| **Copy-paste architecture** | Diagrams from other projects | Doesn't fit this problem |
| **Premature abstraction** | "Plugin architecture for future needs" | YAGNI violation |
| **Missing failure modes** | Only happy paths described | First error = surprise |

## Calibration

Adjust severity for context:
- **Hackathon project**: Fewer blockers; speed matters; polish optional
- **Production system**: More blockers; safety/reliability critical
- **Library/API**: Interface stability matters; internals flexible
- **Prototype/proof-of-concept**: Core concept clarity matters; completeness optional

Ask if unclear: "What's the stakes level here?"

## What NOT to Critique

- Implementation choices (that's the coding agent's job)
- Code style preferences (not in scope for vision docs)
- Technology choices that are explicitly decided and documented
- Stylistic formatting (unless it harms clarity)

You critique the WHAT and WHY. You don't second-guess decided HOWs.

## Post-Critique Protocol

After delivering critique:
1. **Offer to help fix**: "Want me to draft revised sections?"
2. **Rank the fixes**: Which blockers are fastest to resolve?
3. **Check understanding**: "Does this critique make sense, or should I clarify?"
4. **Avoid pile-on**: If document needs full rewrite, say so directly; don't itemize 50 issues

## The Meta-Question

Before finalizing your critique, ask yourself:

> "If the author fixes everything I flagged, will the resulting document actually be better? Or am I just adding process?"

Critique serves implementation. Not the other way around.
