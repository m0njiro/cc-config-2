# Project Setup Instructions
# Run this inside any new project folder to initialise it for Claude Code.
# Run once per new project — each gets its own isolated setup.
# Global setup must be complete before running this.

## Critical Note
All global agents, skills, and rules from ~/.claude/ are automatically available.
This setup only creates project-specific context files.
Do not recreate any global files here — they are already available globally.

## Prerequisites
Confirm before starting:
- [ ] Global setup has already been run and ~/.claude/ is complete
- [ ] You are inside the correct project directory
- [ ] You know the project name and have a rough sense of what it involves

## Step 1 — Gather Project Information
Ask the user for:
1. Project name
2. One paragraph description of what the project does and why it exists
3. File paths: where are the source PDFs / confluence exports?
4. File paths: where is the schema mapping Excel or reference?
5. File paths: where are existing code files or prior session outputs if any?
6. File paths: where should outputs go?
7. Current phase: Migration / Review / Documentation / Governance / New
8. Databases involved: which of DAL / RDE / UDW / Prism does this project touch?
9. Are there any subprojects? If yes, name and brief description of each.

Do not proceed until these are confirmed.

## Step 2 — Create Directory Structure
Inside the current project directory, create:
```
.claude/
.claude/memory/
.claude/memory/daily-log/
reference/
source/
source/existing-work/
track-a-dal-cleanup/
track-a-dal-cleanup/md-working/
track-a-dal-cleanup/html-outputs/
track-a-dal-cleanup/review-findings/
track-b-rde-migration/
track-b-rde-migration/migrated-code/
track-b-rde-migration/migration-log/
prism-udw/
prism-udw/source/
prism-udw/html-outputs/
```

## Step 3 — Create .claude/CLAUDE.md
Use the project CLAUDE.md template from the blueprint.
Fill in all fields using information gathered in Step 1.
If subprojects were identified, add a section per subproject.

## Step 4 — Create Memory Files

Create memory/semantic.md:
```
# Semantic Memory — [Project Name]
Last updated: YYYY-MM-DD

## Domain Facts
[Add permanent truths as discovered and confirmed]

## Confirmed Column Mappings (DAL → RDE)
[Add as confirmed — authoritative list is in reference/schema-mapping.md]

## RDE Constraints Discovered
- RDE requires groupby on all queries — ungrouped access returns error
[Add additional constraints as found during real migration work]

## Governance Rules Confirmed
[Add rules specifically confirmed for this project]

## Code Patterns That Work
[Add patterns that solved specific problems — for reuse in future sessions]

## Code Patterns to Avoid
[Add anti-patterns encountered]

## File Paths Confirmed
[Add confirmed paths as validated — reduces re-discovery overhead]

## Existing Work Assessment
[Notes on quality of prior session outputs found in source/existing-work/]

## Outstanding Questions
[Add open questions — move to relevant section above when resolved]
```

Create memory/episodic.md:
```
# Episodic Memory — [Project Name]
Last updated: YYYY-MM-DD HH:MM

## Current Project
[Project name and one-line description]

## Active Task
None — fresh start

## Session Decisions
[No decisions yet]

## Completed This Session
[Nothing yet]

## Status
NEW

## Next Action
Discuss with user what to tackle first.
Recommended: run plan mode on the simplest PDF to calibrate the workflow.

## Context Used at Last Checkpoint
N/A — fresh session
```

## Step 5 — Build Reference Files

### reference/schema-mapping.md
Ask: "Please provide the path to your schema mapping Excel file."
Read the Excel file.
Extract the DAL → RDE column mapping table.
Create reference/schema-mapping.md:
```
# Schema Mapping — DAL to RDE
# Source: [Excel file name and path]
# Last updated: YYYY-MM-DD

## Column Mappings
| DAL Column Name | RDE Column Name | Notes |
|-----------------|-----------------|-------|
[extracted from Excel]
```

### reference/rde-patterns.md
Create as empty structured template — do not pre-fill with assumed patterns.
Ask: "Have you already confirmed any RDE-specific SQL-to-Python patterns from prior
work? If yes, tell me and I will add them now. Otherwise this fills during migration."
Only add patterns the user explicitly confirms. Never assume.
```
# RDE Patterns — Confirmed SQL to Python Translations
# Add only confirmed patterns — never assume
# Last updated: YYYY-MM-DD

## Confirmed Patterns
| DAL SQL Pattern | RDE Python Equivalent | Confirmed Date |
|-----------------|----------------------|----------------|
[add as confirmed during real migration work]
```

### reference/euc-governance-rules.md
Ask: "Please provide the path(s) to your EUC governance HTML files."
Read the governance HTML files.
Distil the key rules:
```
# EUC Governance Rules
# Source: [HTML file names]
# Last updated: YYYY-MM-DD

## Mandatory Rules (blocking for sign-off)
[extracted from HTML]

## Required Standards (must meet)
[extracted from HTML]

## Recommended Practices (should meet)
[extracted from HTML]
```

### reference/confluence-html-template.md
Ask: "Do you have an existing HTML confluence report I can use as the CSS template?"
If yes: read it, extract CSS classes and structure, document them.
If no: create a standard professional template suitable for Confluence.
Document all classes and structure so html-doc-generator knows exactly what to use.

## Step 6 — Handle Existing Work
Ask: "Do you have any prior session outputs, partial work, or earlier CC outputs
to bring in?"
If yes: note their location in source/existing-work/
Add an entry to memory/semantic.md under Existing Work Assessment.
Do not process them now — evaluated control by control during actual work.

## Step 6b — Create Progress Tracker
Create progress-tracker.md in the project root:
```
# [Project Name] Progress Tracker
Last updated: YYYY-MM-DD

## How to Read This Tracker
- One row per PDF (Confluence page)
- Each PDF contains multiple controls
- Current Control = control number actively being worked on
- All counts are out of Total Controls for that PDF
- Status: NOT STARTED / IN PROGRESS / PARTIAL / REVIEW NEEDED / DONE

## Track A — DAL Cleanup and Confluence Revamp
| PDF Name | Total Controls | Current Control | DAL Cleaned | Issues Flagged | MD Files Done | Full Page HTML | Status |
|----------|---------------|-----------------|-------------|----------------|---------------|----------------|--------|
| [pdf-01] | [N]           | 0               | 0/N         | 0/N            | 0/N           | NO             | NOT STARTED |

## Track B — RDE Migration
| PDF Name | Total Controls | Current Control | RDE Migrated | QA Tested | Migration Logged | Status |
|----------|---------------|-----------------|--------------|-----------|------------------|--------|
| [pdf-01] | [N]           | 0               | 0/N          | 0/N       | 0/N              | NOT STARTED |

## Confluence Page Outputs
| PDF Name | HTML Output Path | Last Updated | Ready for Confluence |
|----------|-----------------|--------------|----------------------|
| [pdf-01] | track-a-dal-cleanup/html-outputs/[pdf-01].html | - | NO |

## Prism vs UDW Subproject
| Task | Status | Output Path | Notes |
|------|--------|-------------|-------|
| [task] | NOT STARTED | | |

## Summary
Total PDFs: [N]
Total Controls (estimated): [N]
Track A Complete: 0/N PDFs
Track B Complete: 0/N PDFs
Ready for Confluence: 0/N pages
```

After creating the tracker, populate PDF Name rows from source/confluence-pdfs/.
Leave all control counts blank — filled in as each PDF is first read.

## Step 6c — Confirm Output Folder Structure
Confirm all folders from Step 2 exist:
```
track-a-dal-cleanup/md-working/     ← MD file per control during processing
track-a-dal-cleanup/html-outputs/   ← one complete HTML per PDF for Confluence
track-a-dal-cleanup/review-findings/
track-b-rde-migration/migrated-code/
track-b-rde-migration/migration-log/
prism-udw/source/
prism-udw/html-outputs/
```

Workflow principle — state this explicitly to confirm understanding:
Per control → write structured MD to md-working/[pdf-name]/
Per PDF when all controls done → merge MDs → one HTML via html-doc-generator
Never generate HTML per individual control — MD during processing, HTML once at end.

## Step 7 — Write Initial Episodic Entry
Update memory/episodic.md:
- Status: NEW → ACTIVE
- Active task: Project initialisation complete
- Next action: Based on current phase from Step 1

Append to memory/daily-log/YYYY-MM-DD.md (create file if first entry today):
```
---
[HH:MM] Project Initialised
Project: [name]
Phase: [phase]
Reference files built: schema-mapping, rde-patterns, euc-governance-rules,
confluence-html-template
Existing work found: [yes — location / no]
PDFs to process: [N files listed in progress-tracker]
Next: [first task based on phase]
---
```

## Step 8 — Confirm to User
Say:
"Project [name] is ready.

Global agents, skills, and rules are already available from ~/.claude/

Project files created:
[list all created files with paths]

Reference files built from:
- Schema mapping: [source file]
- Governance rules: [source file(s)]
- HTML template: [source file or 'standard template created']

[N] PDFs listed in progress-tracker.md ready for processing.

Start your next session with /new-session to load context and begin work.
Recommended first task: Use plan mode on the simplest PDF to calibrate the workflow."
