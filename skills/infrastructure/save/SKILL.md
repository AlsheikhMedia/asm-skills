---
name: save
description: End-of-session progress saver. Updates memory, commits changes, and asks about pushing. Use when the user says "save", "save progress", "wrap up", "end session", or "let's stop here".
disable-model-invocation: true
metadata:
  author: AlSheikh Media
  version: 2.0.0
---

# Save Progress

You are performing an end-of-session save. Complete ALL steps below in order. Do not skip any step.

---

## Step 1: Identify Project Context

Determine the current working directory and its memory path:

- Read the MEMORY.md file for this project (check `~/.claude/projects/` for the matching project path)
- If no MEMORY.md exists, create one with the project name and a summary of what was done

---

## Step 2: Update Memory File

Update MEMORY.md with:

- What was accomplished this session (concise, factual)
- Any new files, patterns, or conventions discovered
- Any gotchas or bugs encountered and how they were resolved
- Updated status of any project milestones
- What was being worked on when the session ended

Do NOT duplicate existing entries. Update existing sections if the information changed. Keep MEMORY.md under 200 lines.

If the project has topic-specific memory files, update those too if relevant.

---

## Step 3: Update Project Docs (if they exist)

Check if the project has any of these common doc patterns and update them if relevant:

- Sprint/status docs (e.g., `docs/sprint-status.md`, `docs/status.md`)
- Roadmap files (e.g., `docs/roadmap.md`, `ROADMAP.md`)
- Changelog (e.g., `CHANGELOG.md`)

Only update docs that already exist and where work was actually done. Do NOT create new doc files unless the project convention requires it. Do NOT update docs with speculative or planned work — only record what was actually done.

If no such docs exist in the project, skip this step entirely.

---

## Step 4: Git Commit

1. Run `git status` to see all changes
2. Run `git diff --stat HEAD` to see the full scope
3. Stage all relevant files (be specific — no `git add .`)
4. Write a clear commit message summarizing the session's work
5. Commit with `Co-Authored-By: Claude <noreply@anthropic.com>`

If there are no changes to commit, say so and skip to Step 5.

---

## Step 5: Ask About Push

After committing, ask the user:

> Committed. Want me to push to remote?

Wait for their answer. Do NOT push without explicit confirmation.

---

## Anti-Patterns

- Do NOT push without asking
- Do NOT create new doc files unless the project convention requires it — update existing ones
- Do NOT bloat MEMORY.md past 200 lines — summarize and link to topic files
- Do NOT update docs with speculative or planned work — only record what was actually done
- Do NOT use `git add .` or `git add -A` — stage specific files
