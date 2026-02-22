# [Project Name] — Project Context
# Created: YYYY-MM-DD

## What This Project Is
[One paragraph: what the project does, why it exists, what problem it solves]

## Important
All global agents, skills, and rules from ~/.claude/ are automatically available
in this project. This file only provides project-specific context.
Do not recreate any global files here.

## Key Files and Paths
- Source PDFs / confluence exports: [path]
- Schema mapping reference: reference/schema-mapping.md
- RDE patterns reference: reference/rde-patterns.md
- EUC governance rules: reference/euc-governance-rules.md
- HTML template: reference/confluence-html-template.md
- Existing work from prior sessions: source/existing-work/
- Output directory: [path]

## Project-Specific Rules
[Any rules that apply only to this project — leave blank if none]

## Databases Involved
- Source: [DAL / RDE / UDW — describe what each contains in this project]
- Target: [what the output connects to or feeds]

## End Goals
Track A — DAL Cleanup and Confluence Revamp:
- Clean every DAL code across all PDFs (indentation, comments, joins, CTEs, filters)
- Flag and log all issues found per control
- Produce one complete revamped HTML Confluence page per PDF
- Each HTML page contains all controls on that page, fully cleaned and structured
- HTML pages are copy-paste ready for Confluence — this is the primary deliverable

Track B — RDE Migration:
- Convert every DAL control to functional RDE Python
- Preserve business logic and output exactly — log any optimisations separately
- Generate pytest suite per migrated control
- Migration runs in parallel with Track A but is secondary priority

## Workflow Principle
Never generate HTML per individual control — write MD during processing,
generate HTML once per PDF at the end when all controls are complete.
This is the token-efficient approach.

## Output Structure
- track-a-dal-cleanup/md-working/[pdf-name]/ ← one MD file per control during processing
- track-a-dal-cleanup/html-outputs/ ← final Confluence-ready HTML pages (one per PDF)
- track-a-dal-cleanup/review-findings/ ← issues flagged per PDF
- track-b-rde-migration/migrated-code/ ← RDE Python per control
- track-b-rde-migration/migration-log/ ← migration change log
- progress-tracker.md ← single source of truth for all progress

## Subprojects
### Prism vs UDW
- Near completion — lives inside codebridge as a subproject
- Uses RDE for querying
- Output: HTML reports in same three-section format (executive, technical, data)
- Source files: prism-udw/source/
- Progress tracked in separate section of progress-tracker.md

## Existing Work Handling
Before processing any control, check source/existing-work/ for prior outputs.
If prior work exists for that control:
- Read it and assess quality against current code-style.md standards
- Ask: would this pass code-reviewer at score 7 or above?
- If yes — use as starting point, note it in the MD file, validate as you go
- If no — process from scratch
Never blindly copy prior work — always validate every assumption

## Key Contacts and Ownership
[Who owns this code, who are the stakeholders, who reviews final output]

## Current Phase
[Migration / Review / Documentation / Governance / Complete]

## Known Issues or Constraints
[Any known blockers, quirks specific to this project's data or code]

## Memory Files
- memory/semantic.md — permanent domain knowledge for this project
- memory/episodic.md — current working state
- memory/daily-log/ — session history
