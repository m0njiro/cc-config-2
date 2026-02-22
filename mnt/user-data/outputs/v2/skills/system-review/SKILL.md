---
name: system-review
description: Full system review covering improvements to existing files and gaps requiring new files. Spawns system-improver and gap-identifier subagents. Run after every 10 controls processed or when quality drift is noticed. Use --deep flag for 30-day log analysis.
---

# System Review Skill

## Purpose
Systematically improve the Claude Code configuration based on real session patterns.
Covers both refining what exists and identifying what is missing.

## Steps

### 1 — Gather Inputs
Collect:
- Last 10 session daily logs from memory/daily-log/ (or last 30 days if --deep flag passed)
- memory/semantic.md
- All current files in ~/.claude/agents/
- All current files in ~/.claude/skills/
- All current files in ~/.claude/rules/
- ~/.claude/CLAUDE.md

### 2 — Spawn system-improver Subagent
Pass all gathered inputs.
Receive structured improvement suggestions report.

### 3 — Spawn gap-identifier Subagent
Pass all gathered inputs.
Receive gap analysis report.

### 4 — Compile Combined Report
Present both reports together clearly separated:

```
SYSTEM REVIEW REPORT — [date]
Sessions analysed: [N]
Mode: [default 10 sessions / deep 30 days]

PART 1 — IMPROVEMENTS TO EXISTING FILES
[system-improver output]

PART 2 — GAPS REQUIRING NEW FILES
[gap-identifier output]

RECOMMENDED PRIORITY ORDER:
[Top 5 actions ranked by impact]
```

### 5 — Get Approval
Ask: "Which of these would you like to act on?
List the item numbers or say all to implement everything recommended.
Say none to skip and close the review."

### 6 — Implement Approved Changes
Work through approved items one at a time.
For each item:
- State what you are about to change and why
- Show the proposed change in full
- Wait for confirmation
- Implement only after explicit confirmation
- Move to next item only after current is confirmed done

Never implement multiple changes simultaneously.
Never implement without per-item confirmation.

### 7 — Checkpoint
After all approved changes are implemented:
- Write episodic checkpoint noting what was changed
- Append to daily log:
  "[HH:MM] /system-review complete — [N] changes implemented: [brief list]"
- State: "System review complete. Next review recommended after [N] more controls."
