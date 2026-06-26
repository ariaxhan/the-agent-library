---
name: agent-tradition
description: Give AI coding agents durable institutional memory — purpose, falsifiable beliefs, narrative lessons, and hook-enforced session accountability — so each session makes the next one smarter instead of starting blind.
---

# Agent Tradition — institutional memory for AI coding agents

## What this is

A small, portable `_meta/` layer you drop into any repo. It gives an AI agent the
three things a new teammate would get on day one but an agent normally never gets:
**why this project exists, what we currently believe works, and the scars from
everything we already tried.** Plain text files, version-controlled, read at the
start of work and written at the end. No service, no database required.

## The problem it solves: agent amnesia

Every session, a coding agent wakes up with zero memory. It re-derives the same
architecture, re-proposes a rejected approach, re-walks a wall someone already
bruised on, and re-learns a lesson that cost real hours last week. The intelligence
is high; the *continuity* is zero. Tradition is the continuity layer — the part of
the mind that persists when the session ends, so judgment compounds instead of
resetting to blank every time.

## The five-file vocabulary

Five files under `_meta/`, each answering a different question. Together they're the
institutional memory; apart, each changes a specific decision.

- **telos.md — WHY this repo exists.** One or two stable sentences of purpose (not
  goals, not tasks). Changes in years, not weeks. It's the spine: it anchors every
  other file and tells an agent what "good" is even aimed at. Example: *"A billing
  service whose single job is to never double-charge a customer."*
- **ethos.md — HOW work behaves unsupervised.** Character, not rules. The disposition
  an agent brings before any specific rule applies — skeptical, evidence-seeking,
  minimal, honest about failure. Inherited and rarely edited. Where a rule is silent,
  ethos decides. Example: *"Verify live; 'committed' is never 'done.'"*
- **doctrine.md — current FALSIFIABLE beliefs.** Each entry is a standing bet:
  **belief · confidence · evidence · what would falsify it · review date.** This file
  is *supposed* to change. The discipline is the falsifier — *an entry with no
  falsifier is faith, not doctrine.* Example: *"Postgres advisory locks are enough for
  our concurrency — falsified if we see a double-write under load test."*
- **canon/ — narrative memory.** Preserved *stories* of failures, breakthroughs, and
  precedents, kept with their **context, conflict, and consequence** — not flattened
  to a one-line rule. A rule says "don't delete that folder"; canon keeps *why someone
  did, what it cost, and how it was recovered*, so the judgment transmits, not just the
  prohibition. If it fits in one line, it belongs in doctrine, not here.
- **phronesis.md — distilled judgment.** Practical wisdom extracted ONLY from patterns
  that **recurred across multiple sessions** — one case is an anecdote, not phronesis.
  Every entry carries its own **"danger of overgeneralizing"** counter-indication, so
  the wisdom doesn't harden into dogma. Example: *"Audit the premise before executing —
  but don't re-litigate well-specified, low-stakes asks."*

## The commission → chronicle work loop

Wrapped around substantial work are two units that turn a session into a reusable
record:

- **Commission** (written BEFORE): the work order. Scope, granted authority, desired
  outcomes-as-end-states (not a step recipe), boundaries, and how "done" gets verified
  live. It grants authority and context, then leaves the path to the agent. If you're
  writing every step, you're writing a plan, not a commission.
- **Chronicle** (written AFTER): the honest "what actually happened" account —
  attempted, changed, **verified-live**, failed, deferred, and any disagreements with
  the ask. Not a success report; it must survive a future reality audit. The disagreements
  and failures are the most valuable part, because that's what the next agent inherits.

## How to make it stick: hooks, not honor-system

Prose rules drift under load — an agent skips the file it was "supposed" to read.
So the loop is **hook-enforced**, not aspirational. Three hooks (full spec in
`reference.md`):

1. **SessionStart — surface.** Prints the telos chain and points the agent at ethos +
   doctrine + canon before any source work. The tradition can't be invisible.
2. **PreToolUse (Write|Edit) — commission-scaffold.** On the first *source* edit of a
   session with no active commission, auto-creates a commission stub. No wall; it
   always allows the edit, it just refuses to let work start untracked.
3. **Stop — chronicle-gate.** A session that changed source **cannot end** until a
   chronicle exists. This is the load-bearing one: it's what forces memory to actually
   get written instead of evaporating with the context window.

## How to adopt it in your repo

1. Create `_meta/` with the five files. Generic fill-in-the-blank templates for all
   five (plus commission + chronicle) are in **`reference.md`** in this folder — copy
   them and replace the bracketed parts.
2. Add the three hooks to `.claude/hooks/` and register them in `.claude/settings.json`
   (SessionStart / PreToolUse `Write|Edit` / Stop). The hook bodies + registration
   JSON are in `reference.md`.
3. Fill in `telos.md` first — it's the spine; the hooks key off its presence.
4. Seed `ethos.md` and `doctrine.md` from the baseline templates; leave `canon/` and
   `phronesis.md` empty. They earn their entries from real sessions.
5. Commit `_meta/`. Never gitignore it — untracked memory is unrecoverable memory.

## What NOT to do

- **Don't flatten canon into rules.** A one-line "don't do X" loses the context that
  makes the judgment transferable. Keep the story.
- **Don't write doctrine without a falsifier.** No "what would prove this wrong" = it's
  faith; move it to ethos or delete it.
- **Don't promote one case to phronesis.** Wait for the pattern to recur, and always
  attach the danger of overgeneralizing.
- **Don't let it become a note-hoard.** A file never read at the moment it would change
  a decision is rot. Every entry earns its place by changing behavior — or it's pruned.
- **Don't write a chronicle that's all wins.** If nothing failed and nothing was
  deferred, you're hiding something the next agent needs.
- **Don't rely on honor-system reading.** If a behavior must hold, it's a hook, not a
  sentence.
