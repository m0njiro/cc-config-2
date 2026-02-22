# Code Style — RDE Patterns and Python Conventions

## Core Principle
Every migration must preserve the original code's business logic and output exactly.
Only the data access layer changes. If in doubt, flag it — never guess.

## RDE Fundamentals
- RDE does not support most SQL functions — use Python/pandas for all complex operations
- RDE always requires a groupby — queries without aggregation will fail
- RDE is accessed via Python — all RDE code is Python, not raw SQL
- RDE column names differ from DAL — always reference schema-mapping.md before migrating

## SQL Functions — DAL vs RDE Equivalent
This table is built up as migrations are completed and patterns are confirmed.
Do not pre-populate with assumptions. When a SQL-to-Python pattern is confirmed working
in your RDE environment, add it here and mirror it in memory/semantic.md.

| DAL SQL Pattern | RDE Python Equivalent | Confirmed Date |
|-----------------|----------------------|----------------|
| [add as confirmed during migration] | | |

## Comment Standards — What to Write and What Not to Write

Write comments that explain why, not what:
- Good: `# RDE requires groupby on all queries — ungrouped access returns error`
- Bad: `# Group the data` or `# This processes the trades efficiently`

Never write:
- Comments that restate what the code obviously does (`# Loop through rows`)
- AI-sounding filler comments (`# This function handles data processing`)
- Complimentary self-narration (`# Elegant solution using pandas merge`)
- Comments that were true of the original DAL code but not the migrated RDE code

Always write:
- A module-level docstring: what the file does, inputs, outputs, owner
- Function docstrings on every function: parameters, return value, purpose
- Inline comments explaining non-obvious business rules or RDE-specific constraints
- A comment whenever a workaround was needed: what the original SQL was and why
  Python was required instead

## Python Code Standards
- Use pandas for all data manipulation — no raw loops over rows
- Import block always: `import pandas as pd`, `import numpy as np` at minimum
- DataFrames named descriptively — not df1, df2 but `trade_data`, `risk_positions`
- Intermediate DataFrames should mirror the CTE they replace in name and purpose
- All groupby operations must explicitly list aggregation columns — no implicit agg
- Functions must do one thing and fit within roughly 20 lines — if longer, split it
- Preserve original SQL comments translated into Python comments

## Code Review Standards
- No redundant filters (same condition applied twice)
- No CTEs or DataFrames created but never used downstream
- Joins must have a clearly justified join key — flag any join on non-unique keys
- Filters on columns post-join must account for nulls introduced by outer joins
- All date filters must be explicit about inclusive/exclusive bounds
- Variable names must be meaningful — single letter variables flagged except loop indices

## File Formatting
- Python files: 4-space indentation, no tabs
- Max line length: 100 characters
- Functions for any logic block over 20 lines
- Docstrings on all functions describing inputs, outputs, and purpose
