---
name: prompt
description: Convert rough text into an optimised Claude Code prompt. Spawns prompt-optimizer subagent. Returns polished prompt for user confirmation before use. Never auto-executes the generated prompt.
---

# Prompt Skill

## Purpose
Take what you want to say and turn it into a properly structured CC prompt
that minimises back-and-forth and token waste.

## Steps

1. Take the rough text provided with /prompt command.
   If no text was provided inline, ask: "What would you like to do?
   Describe it in any way — I will optimise it into a proper prompt."

2. Spawn prompt-optimizer subagent.
   Pass: the rough text only.
   Do not pass session context, project background, or history.
   The optimizer must be stateless.

3. Receive the optimised prompt.

4. Present it to the user:
   "Here is your optimised prompt. Review before using:

   ---
   [optimised prompt]
   ---

   Confirm to use as-is, or tell me what to adjust."

5. On confirmation — the prompt is ready for the user to copy and use.
   Do not execute the prompt automatically.
   Do not act on the prompt content yourself.
   The user decides when and whether to use it.

## Note
The optimised prompt is always a suggestion.
The user always decides whether to use it, modify it, or discard it.
