---
name: bootstrap
description: Mid-session context reload. Re-reads all instruction files without starting a new session. Use when CC seems to be drifting, ignoring rules, or missing the canary word mid-session.
---

# Bootstrap Skill

## Purpose
Reload all instructions mid-session without losing current working context.
This is not the same as /new-session — it does not reset state.
It re-reads the instruction files so CC is back on track.

## Steps in Order

1. Re-read ~/.claude/CLAUDE.md
   Confirm: "Global CLAUDE.md reloaded"

2. Re-read all files in ~/.claude/rules/:
   - guardrails.md
   - memory-protocol.md
   - model-routing.md
   - code-style.md
   - migration-routing.md
   - error-recovery.md
   - workflow-sequences.md
   Confirm: "All 7 rules reloaded"

3. Re-read project .claude/CLAUDE.md if in a project folder
   Confirm: "Project context reloaded: [project name]"

4. Re-read memory/semantic.md
   Confirm: "Semantic memory reloaded"

5. Re-read memory/episodic.md
   Confirm: "Episodic memory reloaded — current status: [status]"

## After Reloading
State: "Bootstrap complete. All instructions reloaded. Resuming: [current task]"
Append Nightjar to confirm canary is active again.
Append a note to memory/daily-log/YYYY-MM-DD.md:
"[HH:MM] Bootstrap triggered — instructions reloaded mid-session"

## Do Not
- Reset episodic state
- Lose track of work completed this session
- Ask the user to re-explain what we were doing
- Start over — reload instructions and continue from exactly where we were
