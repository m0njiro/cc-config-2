# Error Recovery Protocol

## Subagent Returns Error
1. Note the error and which subagent failed
2. Try once more with the same input
3. If it fails again, handle inline with primary agent
4. Log the failure in daily-log with exact error message
5. Flag for /system-review to investigate pattern if it recurs

## PDF Cannot Be Read
1. Note which PDF and what the error is
2. Try reading specific pages rather than the whole PDF
3. If still failing, mark as BLOCKED in progress-tracker.md with reason
4. Move to next PDF — do not get stuck
5. Flag for manual inspection and note in episodic.md

## Migration Produces Potential Output Change
1. Stop immediately — do not proceed
2. Show user exactly what would change and why
3. Wait for explicit confirmation before continuing
4. If confirmed, log the change prominently in migration-log
5. Flag it in the MD file for that control under POTENTIAL OUTPUT CHANGE

## Context Hits 80% Mid-Control
1. Finish the current atomic step only — nothing more
2. Write the MD file for whatever has been completed so far
3. Mark control status as PARTIAL in progress-tracker.md
4. Write episodic checkpoint with STATUS: MID-SESSION-STOP
5. Note exact next step — which control, which step number, what was last completed
6. Tell user to start fresh session with /new-session

## Canary Word Missing Mid-Session
1. Recognise that instructions may not have loaded correctly
2. Run /bootstrap immediately
3. Append Nightjar to next response
4. Log drift in daily-log:
   "[HH:MM] Canary drift detected — bootstrap triggered"

## General Rule
When in doubt about any error situation — stop, explain what happened,
and ask for direction. Never silently work around an error.
Always log errors in daily-log regardless of how they were resolved.
