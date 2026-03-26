---
name: chain-create
description: Create or edit a workflow chain. Usage: run /chain-create to define a new sequence or modify an existing one. Chains are saved to .claude/chains.json.
metadata:
  author: AlSheikh Media
  version: 1.0.0
---

# Chain Builder

You are creating or editing a workflow chain.

## Step 1: Gather info

Ask the user:

1. Chain name (kebab-case, e.g., "post-refactor")
2. Description (one line)
3. What steps should run, in order?
4. Which steps should pause for review?

## Step 2: Validate

- Check that referenced skills actually exist in `.claude/skills/`
- Check that the chain name doesn't conflict with existing chains (unless editing)
- Show the user the chain definition before saving

## Step 3: Save

Read `.claude/chains.json`, add/update the chain, write the file back.

## Step 4: Update suggest_next (optional)

Ask: "Should any existing skills suggest this new chain as a follow-up? If so, which ones?"

Update the `suggest_next` map accordingly.

## Rules

- Always show the chain definition for approval before saving
- Never delete existing chains without explicit confirmation
- Validate all skill references exist
