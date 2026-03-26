---
name: chain
description: Run a predefined workflow chain — multi-step sequences that execute skills in order with optional pause points for review. Use when someone says "run chain", "run the post-deploy chain", "start session chain", "workflow", or references a chain by name.
metadata:
  author: AlSheikh Media
  version: 1.1.0
---

# Chain Runner

You are executing a workflow chain. Chains are multi-step sequences defined in `.claude/chains.json` that run skills, read files, commit code, or update memory — in order, with optional pause points for human review between steps.

## How It Works

A chain is a named sequence of steps. Each step is one of:
- **Invoke a skill** — run another Claude Code skill by name
- **Read files** — read specified files and summarize them
- **Commit** — stage and commit changes with a session summary
- **Update memory** — write results from previous steps to memory
- **Summarize** — produce a summary of findings so far

Steps can pause for review, letting you approve, skip, or stop.

## Step 1: Load the Chain

Read `.claude/chains.json`. If the user specified a chain name, load it. If not, list available chains with descriptions and ask which to run.

If `.claude/chains.json` doesn't exist, tell the user: "No chains defined yet. Use /chain-create to build one, or create `.claude/chains.json` manually."

## Step 2: Execute Steps in Order

For each step in the chain:

1. Announce: **"Step N/Total: [description]"**
2. Execute based on step type:
   - `"skill"` → invoke that skill by name
   - `"action": "read"` → read specified files, summarize contents
   - `"action": "commit"` → git add + commit with session summary
   - `"action": "update-memory"` → update memory file with results from previous steps
   - `"action": "summarize"` → summarize findings from previous steps
3. If `"pause": true` → show results, ask: **"Continue? (y/skip/stop)"**
   - **y** — continue to next step
   - **skip** — skip next step, move to the one after
   - **stop** — end chain here

## Step 3: Summary

After all steps complete (or chain is stopped):

```
Chain: [name] — [completed / stopped at step N]
Steps run: N/Total
Issues found: [count from audit steps, if any]
```

## Step 4: Suggest Next

Check `suggest_next` in chains.json. If the last skill run has suggestions:

> **Suggested next:** /[skill-name] — [reason]

## Rules

- Never skip steps silently
- Always show step progress (Step 2/4, etc.)
- If a skill fails, report it and ask whether to continue or stop
- Don't modify chains.json — use /chain-create for that

## Example: chains.json

```json
{
  "chains": {
    "post-code": {
      "description": "After code changes — review, audit, commit",
      "steps": [
        { "skill": "simplify", "description": "Review code quality", "pause": true },
        { "skill": "launch-readiness", "description": "Check infrastructure gaps", "pause": true },
        { "action": "commit", "description": "Commit if all clean" }
      ]
    },
    "start-session": {
      "description": "Get context at start of work",
      "steps": [
        { "action": "read", "files": ["README.md", "CLAUDE.md"], "description": "Read project context" },
        { "action": "summarize", "description": "What needs doing today" }
      ]
    }
  },
  "suggest_next": {
    "simplify": ["launch-readiness"],
    "launch-readiness": ["save"]
  }
}
```
