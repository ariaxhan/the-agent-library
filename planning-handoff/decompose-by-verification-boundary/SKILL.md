---
name: decompose-by-verification-boundary
description: >-
  Split substantial work into units by verification boundary, not by file or feature.
  Use when planning implementation order, breaking down a big task, or sequencing a
  build: "how should I split this", "what order should I build this in", "break this
  down", "plan the implementation", "where do I start". A unit of work is the smallest
  change with its own gate; if you cannot name the gate for a piece, the piece is too
  big. Produces an ordered plan where every unit lands green before the next starts.
---

# Decompose by Verification Boundary

The natural ways to split work, by file, by feature, by layer, all share a flaw: the pieces
have no independent proof. You build for hours and only find out whether any of it works at
the end, when everything composes. Splitting by **verification boundary** inverts that. Each
unit carries its own gate, lands green, and becomes solid ground for the next one. Observed
across production agent runs, this is the difference between a tree that stays green and a
big-bang integration that fails in ways nobody can attribute.

## 1. Define the unit: smallest change with its own gate

A unit of work is the smallest change that has a named, runnable check proving it works on
its own: a test count ("these 34 new tests pass"), a compile or typecheck, a render check,
a schema validation, a live request. Not a file. Not a feature. A validation module with its
own tests is a unit; "the backend half of search" is not, because nothing can pass or fail
until the frontend half exists.

## 2. The naming test

For each proposed piece, write down its gate before writing any code: the exact command and
the expected result. If you cannot name the gate, the piece is too big or wrongly shaped.
Split it until every piece has one. This test is the whole method; everything else is
consequences of applying it honestly.

## 3. Land each unit green before the next starts

Finish a unit, run its gate, see it pass, commit. Only then start the next. Never stack a
second half-done unit on top of a first, because when something breaks you can no longer
attribute the failure to a change. A composed feature (the route that wires three verified
modules together) is itself a unit, with its own gate: integration tests over the seam.

## 4. Order by risk, not by convenience

Do the riskiest unit first, while judgment and context are freshest: the concurrency seam,
the streaming path, the irreversible migration, the third-party integration nobody has
exercised. Easy visible work first (screens, copy, wrappers) feels productive and teaches
nothing; if the hard part fails, everything built around it was waste. Rank units by "what
would hurt most to discover late" and schedule in that order.

## 5. Decide product questions in writing before building

If a unit contains an open product or design question (what happens on the miss path, which
of two behaviors is correct), decide it in writing before implementation: state the options,
pick one, record where the decision lives. Building both branches "to be safe" doubles the
code and defers the decision to whoever reads it next. A written one-line decision is
cheaper than either branch.

## Anti-patterns

- **Splitting by file or by layer.** "Do the models, then the services, then the routes"
  produces pieces that cannot be verified alone. Split so each piece proves itself.
- **A plan step with no named check.** "Implement search" is not a unit; "search returns
  ranked results for these five fixture queries" is.
- **Starting unit two while unit one is red.** Failures become unattributable and the tree
  stops being trustworthy ground.
- **Convenience ordering.** Doing the pleasant 80% first leaves the risk exactly where it
  started, but with less time and context to absorb it.
- **Deferring a product decision into the code.** Flags, dual paths, and "configurable for
  now" are unmade decisions wearing an abstraction.

## Output

Return an ordered plan where each unit states:

- The change, in one line.
- The gate: exact command or check, plus the expected result (counts where possible).
- Why it sits at this position in the risk order.
- Any product decision it depends on, with the decision made and recorded before the unit starts.
