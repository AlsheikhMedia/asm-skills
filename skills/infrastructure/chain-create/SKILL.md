---
name: chain-create
description: Create or edit a workflow chain — define multi-step sequences that run skills in order. Use when someone says "create a chain", "new workflow", "edit chain", "chain-create", or wants to automate a repeatable sequence of steps.
metadata:
  author: AlSheikh Media
  version: 1.1.0
---

# Chain Builder

You are creating or editing a workflow chain. Chains are saved to `.claude/chains.json` and executed by the `chain` skill.

## Step 1: Gather Info

Ask the user:

1. **Chain name** — kebab-case (e.g., `post-deploy`, `morning-standup`)
2. **Description** — one line explaining when to use it
3. **Steps** — what should run, in order? Each step is one of:
   - `skill` — invoke a skill by name (e.g., `"skill": "launch-readiness"`)
   - `read` — read specific files (e.g., `"action": "read", "files": ["README.md"]`)
   - `commit` — stage and commit changes
   - `update-memory` — update project memory
   - `summarize` — summarize findings so far
4. **Pause points** — which steps should pause for review before continuing?

## Step 2: Validate

- Check that referenced skills exist in `.claude/skills/` (warn if not found — they might be installed later)
- Check the chain name doesn't conflict with existing chains (unless editing)
- Show the complete chain definition for approval before saving

## Step 3: Save

Read `.claude/chains.json` (create if it doesn't exist), add/update the chain, write back.

Example output:

```json
{
  "chains": {
    "post-deploy": {
      "description": "After deploying — verify and update memory",
      "steps": [
        { "skill": "launch-readiness", "description": "Check production readiness", "pause": true },
        { "action": "update-memory", "description": "Record deploy results" }
      ]
    }
  },
  "suggest_next": {}
}
```

## Step 4: Suggest Next (Optional)

Ask: "Should any skills suggest this chain as a follow-up? For example, after running `save`, suggest `post-deploy`?"

If yes, update the `suggest_next` map in chains.json.

## Rules

- Always show the chain definition for approval before saving
- Never delete existing chains without explicit confirmation
- Warn (don't block) if a referenced skill isn't currently installed
