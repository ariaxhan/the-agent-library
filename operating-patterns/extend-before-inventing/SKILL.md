---
name: extend-before-inventing
description: >-
  Search for the existing spine before building anything new. Use when about to create
  a file, module, helper, wrapper, config system, or process: "should I add a new X",
  "where should this live", "build a helper for this", "we need a system for this", or
  when reviewing work that added a parallel version of something that already existed.
  A close match gets extended, not re-implemented; built-in beats library beats custom.
---

# Extend Before Inventing

The most expensive code in a project is the second implementation of something it already
had. Two versions of one idea drift apart, each collects its own bugs, and every future
reader pays to learn which one is real. Observed across production agent runs, agents
invent parallel systems not from need but from search failure: creating felt faster than
finding. This skill makes finding the first move, every time.

## 1. Search first, and mean it

Before creating anything, search the codebase for the thing you are about to build: the
concept, the likely names, the sibling that must have solved this already. Read what you
find. A close match gets **extended** (a parameter, an option, a new case) rather than
re-implemented next to itself. "Close but not exact" is the design prompt, not the permit
to fork: shaping the existing thing to cover your case is the work.

## 2. The precedence order: built-in beats library beats custom

When nothing in the repo covers it, prefer the platform's built-in, then an established
library already in the dependency tree, then a new dependency, and only last a custom
implementation. Before wrapping or replacing a primitive, **prove it is insufficient**:
state what you need, show the primitive cannot do it, and record that. An abstraction
justified by "cleaner" rather than by a demonstrated gap is a liability with good manners.

## 3. New content is data on an existing spine

Most "we need a new system" moments are actually "we have new content". Adding a template,
a rule, an entry, a page, or a case should mean adding **data** to a structure that already
renders or executes it, not building a second structure. If adding one more item requires
new machinery, fix the spine so it takes items as data; do not clone the spine.

## 4. The invention cap: one sanctioned new system per work cycle

Genuinely new systems are sometimes right. Budget them: at most one per work cycle (a
session, a sprint, a commission), chosen deliberately and named as such, with the search
that came up empty recorded. The cap is not against invention; it is against invention as
a reflex. If a second new system feels necessary in the same cycle, that is the signal to
stop and re-examine the first.

## 5. Shorter is the success metric

After a change that touches existing structure, the file should end **shorter or no
longer** than it started, unless the growth is justified in writing. Deletion of a
duplicate path counts as progress and belongs in the report with the same pride as a
feature: every removed parallel implementation is a permanent drop in the cost of
understanding the project.

## Anti-patterns

- **Creating because searching felt slow.** The five minutes saved becomes a permanent tax.
- **Forking a near-match** instead of extending it. Two copies never converge again.
- **Wrapping a primitive you have not proven insufficient.** The wrapper hides the
  primitive's real API and adds a surface nobody asked for.
- **Building machinery to hold one item.** One item is content; put it on the spine.
- **A "quick parallel version just for now".** There is no such thing; parallel versions
  are permanent the moment a second caller appears.

## Output

Return, for each new artifact proposed or reviewed:

- The search performed and what it found (or that it found nothing).
- The decision: extended existing / built-in / existing library / new dependency / custom, with the insufficiency proof where required.
- Whether the invention cap for this cycle is already spent, and by what.
- Net line delta for touched files, with justification if anything grew.
- Any duplicate path deleted, called out as progress.
