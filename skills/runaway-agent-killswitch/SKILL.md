---
name: runaway-agent-killswitch
description: Stop a looping or runaway autonomous AI agent from burning budget overnight with a fail-open PreToolUse killswitch that hard-caps a Claude Code session by tool-call count and wall-clock time while still letting it checkpoint and exit cleanly.
---

# Runaway Agent Killswitch

## What this is

A `PreToolUse` hook that hard-caps how much a single Claude Code session can do, so a
stuck or looping agent can't burn money or churn overnight. It fires once per tool call —
the only enforcement point *outside* the model's own loop. Over the cap it blocks new
**expensive** tools but keeps a **save-work allowlist** open, so the agent can commit,
write a handoff, and stop without losing work.

Honor-system "please stop at $X" instructions are worthless when an agent is wedged in a
retry loop. Real incidents that motivate this: thousands of redundant tool calls overnight,
deep sub-agent recursion, four-figure spend before anyone woke up. A hook is the one thing
the agent can't talk itself out of.

## When you need it

- Any **overnight / unattended** autonomous run (forge-style loops, agentic batch jobs).
- Any session that can **spawn sub-agents** or fire network/build tools in a loop.
- Long tier-2/tier-3 work you walk away from. If a human isn't watching every tool call,
  arm this.

## The design: cap on COUNT + DURATION, never on cost

Two reliable signals, both checked on every call:

- **Tool-call count per session** — an atomic per-session counter, incremented once per
  call. High-confidence, hard to fake. This is the primary cap.
- **Wall-clock duration** — session start epoch recorded on first call, compared against a
  max-seconds budget (~1s precision).

It deliberately does **NOT** cap on dollars. There is no trustworthy cost signal inside a
hook: the transcript's token fields are broken placeholders that can report **100x lower
than actual** spend, so a dollar budget built on them would be off by two orders of
magnitude. Tool-call count is the honest proxy. Size the default generously (e.g. 500
calls / 2h) so a legitimately long forge doesn't false-trip, but a true runaway hits the
wall.

## The save-work allowlist (permitted even over-cap)

Going over the cap must not strand the agent's work. So when over budget, these still pass:

- `Read`, `Write`, `Edit`, and your todo/notes tool — read state, write a handoff or
  chronicle.
- `Bash` **only** when the command (after stripping leading `VAR=val` env prefixes) starts
  with a save/report verb: `git commit`, `git add`, `git push`, `git status`, `git diff`,
  `git log`, your memory-CLI write, `echo`, `cat`.
- The match is **prefix-anchored**, so `git clone` / `git config` do *not* sneak through the
  `git commit` allowance.

Everything else over-cap is blocked: general `Bash` (builds, installs, tests, `curl`),
`WebSearch`, `WebFetch`, and `Task`/sub-agent spawns. The block message tells the model
exactly how to checkpoint and end.

## The three rules you must NOT get wrong

These three are catastrophic if inverted. They are the whole reason this is hard.

1. **FAIL OPEN on any internal error.** This hook runs on *every* tool call. A safety gate
   that fails *closed* bricks all work the moment it hits a bug. So every internal failure —
   missing `jq`, unparseable stdin, no `session_id`, unwritable state dir, lock timeout,
   corrupt counter — must `exit 0` (allow) with a stderr note. The **only** `exit 2` (block)
   path is a confirmed over-cap read of a successfully-incremented counter against a
   non-allowlisted tool. Do not source shared helper libs into it either: a safety gate must
   always run and never inherit a bug from common code.

2. **PreToolUse, NEVER Stop.** Wire this to `PreToolUse` only. Do **not** put it on the
   `Stop` hook. A `Stop` hook that exits non-zero forces Claude to **keep working** — the
   exact opposite of a killswitch. Blocking forward tool calls at `PreToolUse` is what makes
   a capped agent run out of tools and actually stop.

3. **Sweep stale counters on SessionStart.** A `SessionStart` hook must reset *this*
   session's counter to 0 (preserving it only on `source == "resume"`) and delete state
   files older than ~24h. Without the sweep, a fresh session can inherit a stale over-cap
   counter from a dead session and get instantly bricked before doing any work.

## How to install it

1. Drop `killswitch.sh` somewhere in your repo (e.g. `.claude/hooks/`) and a companion
   `killswitch-init.sh` for SessionStart. `chmod +x` both. (Reference implementations:
   `killswitch.sh.example` next to this skill.)
2. Register them in your Claude Code settings (`.claude/settings.json`), matcher `""` =
   all tools:

   ```json
   {
     "hooks": {
       "PreToolUse":  [{ "matcher": "", "hooks": [{ "type": "command", "command": "$CLAUDE_PROJECT_DIR/.claude/hooks/killswitch.sh" }] }],
       "SessionStart": [{ "matcher": "", "hooks": [{ "type": "command", "command": "$CLAUDE_PROJECT_DIR/.claude/hooks/killswitch-init.sh" }] }]
     }
   }
   ```
3. Tune via env vars: `KILLSWITCH_MAX_TOOLS` (default 500), `KILLSWITCH_MAX_DURATION`
   seconds (default 7200, `0` disables), `KILLSWITCH_WARN_PERCENT` (default 80, emits one
   soft stderr nudge). Escape hatch: `KILLSWITCH_OFF=1` or an override file. State lives in
   `$CLAUDE_PROJECT_DIR/.claude/.killswitch/` (or `$TMPDIR/claude-killswitch/`), keyed by
   `session_id` so multiple windows are naturally isolated.
4. Verify live: start a session, run a few tools, confirm `<session_id>.count` increments;
   set `KILLSWITCH_MAX_TOOLS=3` and confirm tool 4 is blocked while `git commit` still passes.

## Pair it with a hard budget cap

The killswitch is a backstop, not the only control. **Always also set a `max_budget_usd`
ceiling** on any autonomous loop. The budget cap is the dollar guarantee; the killswitch is
the runtime guarantee that survives broken cost telemetry. Run both — that's the point.
