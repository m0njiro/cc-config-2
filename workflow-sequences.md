# Workflow Sequences

## How Major Workflows Chain Together

### Single Code Migration (/migrate skill)
1. Primary agent reads migration-routing.md — confirms inline route
2. Reads reference/schema-mapping.md and reference/rde-patterns.md
3. Migrates inline, producing cleaned Python RDE code
4. Optionally spawns qa-tester subagent if user confirms
5. Writes checkpoint

### PDF Batch Migration (dal-rde-migrator subagent)
1. Primary agent reads migration-routing.md — confirms subagent route
2. Spawns dal-rde-migrator subagent with PDF path and reference files
3. Receives migrated code block by block
4. Optionally spawns qa-tester per block
5. Writes checkpoint after every 3 blocks

### PDF Control Processing (Track A + B combined)
1. Primary agent extracts control list from PDF — confirms with user
2. Per control in sequence:
   a. Extract DAL code inline
   b. Spawn code-reviewer subagent
   c. Spawn euc-governance-checker subagent
   d. Primary agent cleans DAL code inline after confirmation
   e. Spawn dal-rde-migrator subagent for RDE migration
   f. Spawn qa-tester subagent on migrated code
   g. Primary agent writes MD file to track-a-dal-cleanup/md-working/[pdf]/
   h. Primary agent logs migration to track-b-rde-migration/migration-log/
   i. Updates progress-tracker.md
   j. Writes checkpoint
3. After all controls in PDF complete:
   a. Primary agent compiles all MD files for that PDF
   b. Spawns html-doc-generator subagent with compiled content
   c. HTML saved to track-a-dal-cleanup/html-outputs/[pdf-name].html
   d. Updates progress-tracker.md — Full Page HTML = YES
   e. Writes checkpoint

### Code Review (/review skill)
1. Spawns code-reviewer subagent — stateless, code only
2. If --governance flag: also spawns euc-governance-checker subagent
3. If --report flag: spawns html-doc-generator with findings
4. Presents combined findings
5. Writes checkpoint

### Yearly Review (/yearly-review skill)
1. Reads PDF, extracts all code blocks, lists them
2. Confirms list with user
3. Per code block: code-reviewer → euc-governance-checker → improvements → RDE rewrite
4. Writes MD per block (not HTML)
5. After all blocks: spawns html-doc-generator for full report
6. Checkpoints after every 3 blocks

### System Review (/system-review skill)
1. Spawns system-improver subagent
2. Spawns gap-identifier subagent
3. Compiles combined report
4. User approves items
5. Implements one at a time with confirmation
6. Writes checkpoint

## Handoff Rules Between Steps
- Always confirm list or plan with user before processing begins
- Always show original before showing cleaned or migrated version
- Always wait for confirmation at each step gate
- Never spawn next subagent until current one's output is confirmed
- Always write MD or log before writing checkpoint
- Always write checkpoint before ending session or switching PDF
