# Claude Code — Global Configuration
# Last updated: see memory/daily-log for session history

## Who I Am and What I Do
I am a data analyst working in credit risk and data governance at an enterprise level.
My primary work involves SQL-based code migration (DAL to RDE), code quality review,
EUC governance compliance, and generating Confluence-ready documentation.
I work on a single office machine using Claude Code via PyCharm IDE and its terminal.
Enterprise API plan with a $50/day token budget — efficiency is critical.

## How to Start Every Session
1. Check if a project `.claude/` folder exists in the working directory
2. If yes: read `.claude/CLAUDE.md`, then `memory/semantic.md`, then `memory/episodic.md` — in that order
3. If no project context: ask me which project or workflow we are working on before doing anything else
4. Confirm what you have loaded and what the current episodic state says before taking any action

## Rules — Always Apply These
@rules/guardrails.md
@rules/memory-protocol.md
@rules/model-routing.md
@rules/code-style.md
@rules/migration-routing.md
@rules/error-recovery.md
@rules/workflow-sequences.md

## Available Skills
- `/checkpoint` — write memory checkpoint immediately
- `/migrate` — run inline single code block migration (DAL to RDE)
- `/review` — trigger code review subagent
- `/yearly-review` — orchestrate full yearly code review workflow
- `/new-session` — explicit session start, loads all memory files
- `/bootstrap` — mid-session context reload without losing state
- `/prompt` — convert rough text into optimised CC prompt
- `/system-review` — full system improvement and gap analysis

## Available Subagents
Located in `~/.claude/agents/`:
- `code-reviewer` — stateless code quality scorer
- `euc-governance-checker` — stateless EUC governance compliance checker
- `qa-tester` — stateless pytest generator
- `dal-rde-migrator` — batch PDF migration subagent
- `html-doc-generator` — Confluence HTML report generator
- `system-improver` — session pattern analyser and improvement suggester
- `prompt-optimizer` — rough text to optimised CC prompt converter
- `code-restructurer` — monolith to proper project structure converter
- `gap-identifier` — identifies missing skills, agents, and rules

## Critical Constraints — Never Violate
- Never execute database connections (pyodbc or otherwise) autonomously
- Never modify files outside the current project directory without explicit confirmation
- Never run code that touches Prism files or UDW directly
- Always propose code changes, never apply them without confirmation
- If uncertain about any action involving data or files — stop and ask

## Canary — Proof You Read This File
End every response during a migration or review workflow with the word: **Nightjar**
If this word is absent from a response during active workflow, I will know instructions
were not loaded correctly and will restart the session.
Exception: casual conversation, clarifying questions, and session start confirmation
do not require the canary.

## Canary Recovery
If you realise mid-session that you have not been appending Nightjar to active workflow
responses, immediately:
1. Run /bootstrap to reload all instructions
2. Append Nightjar to your very next response
3. Append a note to memory/daily-log/YYYY-MM-DD.md:
   "[HH:MM] Canary drift detected — instructions reloaded via bootstrap"
Do not wait until end of session. Catch and recover immediately.

## Token Budget Awareness
Before starting any heavy task — PDF processing, batch migration, yearly review,
or any task involving more than 3 subagent spawns — estimate whether it fits within
remaining session context. State the estimate explicitly:
"Estimated context required: ~X%. Current available: ~Y%.
Proceeding / Recommending we start fresh session first."
If remaining context is below 40%, do not start a heavy task.
Finish current work, write checkpoint, flag for next session.
