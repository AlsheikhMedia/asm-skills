---
name: chain
description: Run a predefined workflow chain. Usage: run /chain then specify which chain (post-code, post-deploy, start-session, post-copy). Chains are multi-step sequences that run skills in order with optional pause points for review.
metadata:
  author: AlSheikh Media
  version: 1.0.0
---

# Chain Runner

You are executing a workflow chain. Follow these steps exactly.

## Step 1: Identify the chain

Read `.claude/chains.json`. The user will specify which chain to run (post-code, post-deploy, start-session, post-copy).

If the user didn't specify which chain, list available chains with descriptions and ask which one to run.

## Step 2: Execute steps in order

For each step in the chain:

1. Announce: "**Step N/Total: [description]**"
2. If step has `"skill"`: invoke that skill by name
3. If step has `"action": "read"`: read the specified files and summarize
4. If step has `"action": "commit"`: run git add + commit with a summary of the session's changes
5. If step has `"action": "update-memory"`: update the memory file with results from previous steps
6. If step has `"action": "summarize"`: summarize findings from previous steps
7. If step has `"pause": true`: after completing the step, show results and ask "Continue to next step? (y/skip/stop)"
   - y: continue
   - skip: skip next step, move to the one after
   - stop: end chain here

## Step 3: Summary

After all steps complete (or chain is stopped), print:

```
Chain: [name] — [completed/stopped at step N]
Steps run: N/Total
Issues found: [count from audit steps, if any]
```

## Step 4: Suggest next

Check `suggest_next` in chains.json. If the last skill run has suggestions, print:

> **Suggested next:** /[skill-name] — [reason based on what was just done]

## Rules

- Never skip steps silently
- Always show step progress (Step 2/4, etc.)
- If a skill fails or errors, report it and ask whether to continue or stop
- Don't modify chains.json from this skill — use /chain-create for that
