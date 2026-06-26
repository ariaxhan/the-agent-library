# Agent Tradition — adoption reference

Everything you need to stamp a repo with the tradition: the five institutional file
templates, the two work-unit templates (commission + chronicle), and the three hooks
(what each does, when it fires, and the registration JSON). All templates are generic
— replace anything in `<…>` or `[…]`.

Target layout:

```
your-repo/
├── _meta/
│   ├── telos.md
│   ├── ethos.md
│   ├── doctrine.md
│   ├── phronesis.md
│   ├── canon/
│   │   ├── index.md
│   │   ├── failures/
│   │   ├── breakthroughs/
│   │   └── precedents/
│   ├── commissions/
│   │   ├── active/
│   │   └── complete/
│   └── chronicles/
│       └── <year>/
└── .claude/
    ├── hooks/
    │   ├── tradition-surface.sh
    │   ├── commission-scaffold.sh
    │   └── chronicle-gate.sh
    └── settings.json
```

---

## 1. The five institutional files

### `_meta/telos.md` — WHY this exists

```markdown
---
kind: telos
stability: high — change rarely, and only deliberately
---

# Telos — why this exists

> Purpose, not goals and not tasks. One or two sentences answering *why does this
> exist?* Stable: should change in years, not weeks. This is the spine — the hooks
> key off its presence and it anchors every other file.

**<One or two sentences: why this project exists and what it is FOR.
e.g. "A payments service whose single job is to never double-charge a customer.">**

## What this implies (and forbids)
- <A standard this purpose holds work to.>
- <Something this purpose explicitly rules out.>
```

### `_meta/ethos.md` — HOW work behaves unsupervised

```markdown
---
kind: ethos
stability: high — character changes slowly
note: universal baseline; override a line only if this repo's character genuinely differs
---

# Ethos — the character of operation

> How work should behave when nobody is supervising — the disposition before any
> specific rule applies. Where a rule is silent, ethos decides.

**Skeptical · evidence-seeking · minimal · honest about failure · generous with context · allergic to silent rot.**

- **Skeptical of the ask, not just the answer.** The premise can be wrong. Question it
  before acting; act on the better answer and log the disagreement.
- **Verify live — "committed" is not "done."** Run the command that proves it.
  Committed ≠ pushed ≠ deployed ≠ working. Can't check headlessly → "deployed, your check."
- **Minimal — boring beats clever.** Smallest viable change; built-in > library > custom.
- **Honest about failure — degradation must report itself.** No silent error suppression
  on load-bearing paths. When reality contradicts your assumption, halt and surface it.
- **Investigate before mutating.** Before deleting/moving/overwriting anything you didn't
  create this session, verify what it is. Empty/unexpected = investigate, not tidy.
- <Add a repo-specific trait only if this project's character truly differs.>
```

### `_meta/doctrine.md` — current FALSIFIABLE beliefs

```markdown
---
kind: doctrine
stability: provisional — this file is SUPPOSED to change
---

# Doctrine — current best understanding of what works

> Each entry is a standing bet carrying its own falsifier. When canon and reality
> contradict doctrine, doctrine yields — that's the design. An entry with no falsifier
> is faith, not doctrine; it belongs in ethos or nowhere.

Each entry: **belief · confidence · evidence · what would falsify it · review date.**

## D1 · <short claim>
**Belief:** <the bet, stated so it could be wrong.>
**Confidence:** <low / medium / high.>
**Evidence:** <what observation supports it today.>
**Falsifies it:** <the concrete observation that would prove this wrong.>
**Review:** <YYYY-MM-DD.>

## D2 · <short claim>
**Belief:** … **Confidence:** … **Evidence:** … **Falsifies it:** … **Review:** …
```

### `_meta/canon/index.md` — narrative memory

```markdown
---
kind: canon-index
add_via: a copy of the canon-entry template below
---

# Canon — index

> Memory through narrative: the stories future sessions should remember — failures
> with consequence, breakthroughs, precedents. Keep the context/conflict/consequence
> so judgment transmits. If it fits in one line, it belongs in doctrine, not here.

**Before substantial work:** skim this index for a similar story.
**To add:** write the entry under the matching class, register it below.

## Registry
### failures
*(none yet)*
### breakthroughs
*(none yet)*
### precedents
*(none yet)*
```

A single canon entry (`_meta/canon/failures/<slug>.md`):

```markdown
---
kind: canon-entry
class: failure | breakthrough | precedent
date: <YYYY-MM-DD>
keywords: <comma-separated, for retrieval>
---

# <title>

## Context
<What was going on. Enough that a stranger understands the setup.>

## Conflict
<What broke, was discovered, or was decided — and the tension in it.>

## Consequence
<What it cost or unlocked, and what the right move turned out to be.>

## Why this is preserved as a story (not a one-line rule)
<The judgment a flattened rule would lose.>
```

### `_meta/phronesis.md` — distilled judgment

```markdown
---
kind: phronesis
stability: slow-growing — accrues from repeated cases, rarely retracted
guard: one case is an anecdote. Extract only what recurred across MULTIPLE chronicles.
---

# Phronesis — practical wisdom from lived cases

> Judgment, not facts and not summaries — what an experienced operator knows that no
> checklist captures. Earns its slot only by recurring. Every entry carries its own
> danger of overgeneralizing.

## P1 · <short judgment>
**Judgment:** <the practical wisdom, stated as guidance.>
**Drawn from:** <the multiple cases that produced it — at least two.>
**Pattern:** <the recurring shape underneath them.>
**Danger of overgeneralizing:** <when this advice is WRONG / where not to apply it.>
**Future use:** <the concrete question to ask next time it's relevant.>
```

---

## 2. The work-unit templates

### Commission — written BEFORE substantial work

`_meta/commissions/active/<YYYY-MM-DD>-<slug>.md`:

```markdown
---
kind: commission
status: active
commissioned: <YYYY-MM-DD>
on_complete: move to ../complete/ and link its chronicle
---

# Commission — <title>

> Grants authority and context, states desired outcomes, leaves the path to the runner.
> If you're writing every step, you're writing a plan — state the outcome instead.

## Telos of this commission
<Why this work exists. One or two sentences. Can't state why → don't commission it.>

## Authority granted
<What the runner may do without asking: repos, destructive ops, spend, proceeding past ambiguity.>

## Boundaries
<Hard limits. What must NOT be touched/moved/deleted/shipped. Facts to trust, not re-derive.>

## Context
<What the runner needs and can't easily discover: locked decisions, prior attempts, where to start.>

## Desired outcomes
<End states, not tasks. For each: OUTCOME · LOOK AT (where to start) · how it'll be VERIFIED live.>

## Questions to challenge
<Adversarial prompts: is this the right outcome? what would make it a waste? Act on the better answer.>

## Verification standard
<How "done" is proven. Default: verified live, or a DEFERRED note naming the human residual.>
```

### Chronicle — written AFTER

`_meta/chronicles/<year>/<YYYY-MM-DD>-<slug>.md`:

```markdown
---
kind: chronicle
commission: <link to the commission it answers, or "none — ad hoc">
runner: <model / session>
date: <YYYY-MM-DD>
---

# Chronicle — <title>

> The honest account of what happened, not a success report. It must survive a future
> reality audit. If everything went perfectly, you're probably hiding something.

## What was attempted
<The real goals taken on, and where this diverged from the commission and why.>

## What changed
<Concrete deltas: files, configs, deploys, decisions. Paths and commit hashes.>

## What was verified (live)
<For each user-facing claim: the command/check that proved it. "Committed" is not verification.>

## What failed
<Honest. What didn't work, what was wrong in the plan, what you got wrong mid-flight.>

## What was deferred
<Anything left undone, with the exact residual and where it's tracked.>

## Disagreements
<Where you pushed back on the ask and the call you made. The most valuable section.>

## Lessons that may enter canon / phronesis
<Candidate stories (canon) or repeated judgments (phronesis). Only name them; write separately.>
```

---

## 3. The three hooks

All three are self-contained POSIX shell, depend only on `python3` (no `jq`), and use
`$CLAUDE_PROJECT_DIR` (the repo root) so they work standalone or nested. Put them in
`.claude/hooks/` and `chmod +x`.

### a. `tradition-surface.sh` — fires on **SessionStart**

**What it does:** at the start of every session, prints a short pointer block — the
telos one-liner (walking up parent directories so it works in a monorepo too), and a
reminder to read `ethos.md` + `doctrine.md` + skim `canon/` before source work, plus a
note that a chronicle will be required. It also clears the stale per-session marker so
the chronicle gate re-arms cleanly. If the repo has no `_meta/telos.md` or `ethos.md`,
it stays silent and costs nothing. **Why:** the tradition can't be invisible — if the
agent never sees it, it never reads it.

### b. `commission-scaffold.sh` — fires on **PreToolUse** (matcher `Write|Edit`)

**What it does:** on the **first source edit** of a session (anything outside `_meta/`
and `.claude/`), if no commission is active in `_meta/commissions/active/`, it writes a
commission stub there and drops a per-session marker (`_meta/.tradition-session`) that
arms the chronicle gate. **It never blocks the edit** — it always allows the write; it
just refuses to let substantial work begin untracked. Edits to `_meta/` or `.claude/`
don't trigger it. **Why:** scope and intent get captured at the moment work starts,
not reconstructed afterward.

### c. `chronicle-gate.sh` — fires on **Stop**

**What it does:** when the session tries to end, checks the marker. If source was
touched this session and **no chronicle was written/updated after** the marker
timestamp, it returns `{"decision":"block", "reason": …}` and steers the agent to write
a chronicle (attempted / changed / verified-live / failed / deferred / disagreements)
before finishing. Once a fresh chronicle exists it disarms the marker and allows the
stop. If no source was touched, it allows the stop immediately. **Why:** this is the
load-bearing hook — it's what forces memory to actually get written instead of
evaporating with the context window.

### Registration — merge into `.claude/settings.json`

```json
{
  "hooks": {
    "SessionStart": [
      { "hooks": [ { "type": "command", "command": "$CLAUDE_PROJECT_DIR/.claude/hooks/tradition-surface.sh" } ] }
    ],
    "PreToolUse": [
      { "matcher": "Write|Edit", "hooks": [ { "type": "command", "command": "$CLAUDE_PROJECT_DIR/.claude/hooks/commission-scaffold.sh" } ] }
    ],
    "Stop": [
      { "hooks": [ { "type": "command", "command": "$CLAUDE_PROJECT_DIR/.claude/hooks/chronicle-gate.sh" } ] }
    ]
  }
}
```

### Reference hook implementations

`tradition-surface.sh`:

```bash
#!/bin/bash
# SessionStart — surface the tradition (cascade-aware). Pointer only; content read on demand.
set -eo pipefail
ROOT="${CLAUDE_PROJECT_DIR:-$PWD}"
rm -f "$ROOT/_meta/.tradition-session" 2>/dev/null || true          # re-arm gate
[ -f "$ROOT/_meta/ethos.md" ] || [ -f "$ROOT/_meta/telos.md" ] || exit 0

chain=""; dir="$ROOT"
while [ "$dir" != "/" ] && [ -n "$dir" ]; do
  if [ -f "$dir/_meta/telos.md" ]; then
    line=$(grep -m1 -vE '^\s*$|^---|^#|^>|^[a-z_]+:' "$dir/_meta/telos.md" 2>/dev/null \
           | sed 's/^[[:space:]]*//' | cut -c1-140)
    chain="  • **$(basename "$dir")** — ${line}\n${chain}"
  fi
  dir=$(dirname "$dir")
done

echo ""
echo "## Tradition (default operating mode)"
[ -n "$chain" ] && { echo "Telos chain (general → specific):"; printf "%b" "$chain"; }
echo "BEFORE source work: read _meta/ethos.md + _meta/doctrine.md; skim _meta/canon/index.md."
echo "Substantial work = a commission (auto-scaffolds in _meta/commissions/active/)."
echo "AFTER source changes: a chronicle in _meta/chronicles/<year>/ is REQUIRED (Stop gate enforces it)."
echo ""
exit 0
```

`commission-scaffold.sh`:

```bash
#!/bin/bash
# PreToolUse (Write|Edit) — scaffold a commission on first SOURCE edit. No wall; always allows.
set -eo pipefail
ROOT="${CLAUDE_PROJECT_DIR:-$PWD}"; ACTIVE="$ROOT/_meta/commissions/active"
ls "$ACTIVE"/*.md >/dev/null 2>&1 && exit 0
[ -f "$ROOT/_meta/ethos.md" ] || [ -f "$ROOT/_meta/telos.md" ] || exit 0

INPUT=$(cat)
EDITED=$(printf '%s' "$INPUT" | python3 -c "import sys,json
try: print(json.load(sys.stdin).get('tool_input',{}).get('file_path',''))
except Exception: print('')" 2>/dev/null)
case "$EDITED" in ""|*/_meta/*|*/.claude/*) exit 0 ;; esac

mkdir -p "$ROOT/_meta" "$ACTIVE" 2>/dev/null || true
[ -f "$ROOT/_meta/.tradition-session" ] || date +%s > "$ROOT/_meta/.tradition-session"
STUB="$ACTIVE/$(date +%Y-%m-%d)-session.md"
if [ ! -f "$STUB" ]; then
  cat > "$STUB" <<EOF
---
kind: commission
status: active (AUTO-SCAFFOLDED — fill this in)
commissioned: $(date +%Y-%m-%d)
---

# Commission — <name it from the work in flight>

> Auto-created because source changed with no active commission. Steering wheel, not a wall.
> Fill in: telos (why) · outcomes (what good looks like) · boundaries · verification (live).
> A chronicle in _meta/chronicles/$(date +%Y)/ is REQUIRED before the session can end.
EOF
  echo "[tradition] No active commission — scaffolded $STUB. Fill it in; a chronicle is required before session end." >&2
fi
exit 0
```

`chronicle-gate.sh`:

```bash
#!/bin/bash
# Stop — a session that changed source cannot end until a chronicle is written this session.
set -eo pipefail
ROOT="${CLAUDE_PROJECT_DIR:-$PWD}"; MARKER="$ROOT/_meta/.tradition-session"
[ -f "$MARKER" ] || exit 0                                            # no source touched → allow

CHRON="$ROOT/_meta/chronicles"
if [ -d "$CHRON" ] && [ -n "$(find "$CHRON" -name '*.md' -newer "$MARKER" 2>/dev/null | head -1)" ]; then
  rm -f "$MARKER" 2>/dev/null || true; exit 0                         # fresh chronicle → allow + disarm
fi

YEAR=$(date +%Y)
cat <<EOF
{"decision":"block","reason":"This session changed source but no chronicle was written. Before finishing, write _meta/chronicles/${YEAR}/<date>-<slug>.md: what was attempted, what changed, what was VERIFIED LIVE, what failed, what's deferred, any disagreements. Chronicles are how the next session inherits judgment."}
EOF
exit 0
```

---

## Adoption checklist

- [ ] `_meta/` created with all five files (telos filled first — it arms the hooks).
- [ ] `canon/index.md` + `phronesis.md` left empty; they earn entries from real sessions.
- [ ] Three hooks in `.claude/hooks/`, `chmod +x`, registered in `.claude/settings.json`.
- [ ] `_meta/` committed (never gitignored — untracked memory is unrecoverable).
- [ ] First session: confirm SessionStart surfaces the telos, and Stop blocks until a chronicle exists.
