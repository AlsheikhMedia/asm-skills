# GitHub Issues — Task Tracking Reference

This reference covers how the impact skill creates and manages GitHub Issues for cross-departmental task tracking.

## Label Convention

Create these labels on first use (if they don't exist):

**Type:**
- `impact` — all impact-generated issues get this
- `tracking` — the parent/epic issue only

**Department:** `dept-product`, `dept-dev`, `dept-qa`, `dept-design`, `dept-marketing`, `dept-devops`, `dept-sales`, `dept-cs`, `dept-legal`, `dept-finance`, `dept-research`, `dept-analytics`, `dept-security`, `dept-brand`

**Priority:** `p0-blocker`, `p1-parallel`, `p2-followup`

**Phase:** `phase-1`, `phase-2`, `phase-3`

## Tracking Issue Template (Epic)

One per initiative. Links to all department issues.

```markdown
# Impact: [Initiative Name]

**Scope:** [1-line description]
**Created:** [date]
**Departments:** [count] affected
**Status:** 0/[N] complete

## Progress
- [ ] #NNN [Department]: [Key deliverable summary]
- [ ] #NNN [Department]: [Key deliverable summary]

## Dependency Chain
[Department A] (#NNN) → [Department B] (#NNN) → [Department C] (#NNN)
                                                  ↘ [Department D] (#NNN) (parallel)

## Timeline
Critical path: [X-Y days] | Stated deadline: [Z]
```

Labels: `impact`, `impact-{slug}`, `tracking`

## Department Issue Template

One per affected department. Contains that department's deliverables.

```markdown
## [Department] — [Initiative Name]

**Priority:** Blocking / Parallel / Follow-up
**Estimate:** [range]
**Phase:** [1/2/3]

### Deliverables
- [ ] [Specific item with enough detail to act on]
- [ ] [Specific item]

### Blocked By
- #NNN ([Department] — [what specifically])

### Unblocks
- #NNN ([Department] — [what they're waiting for])

### Progress
[Updated each session with what was done]
```

Labels: `impact`, `impact-{slug}`, `dept-{name}`, `phase-{n}`, `p0-blocker` / `p1-parallel` / `p2-followup`

## Commands Reference

### Create issues

```bash
# Create tracking issue
gh issue create --title "Impact: [Initiative Name]" \
  --label "impact,impact-{slug},tracking" \
  --body-file /tmp/impact-tracking.md

# Create department issue
gh issue create --title "[Dept]: [Key deliverable] — [Initiative]" \
  --label "impact,impact-{slug},dept-{name},phase-{n},p{priority}" \
  --body-file /tmp/impact-dept.md
```

### List open impact issues

```bash
# All open impact issues for current repo
gh issue list --label impact --state open --json number,title,labels

# Filter by initiative
gh issue list --label impact-{slug} --state open --json number,title,labels,body

# Filter by department
gh issue list --label dept-dev --label impact --state open

# Filter by phase
gh issue list --label phase-1 --label impact --state open
```

### Update progress

```bash
# Add progress comment
gh issue comment {number} --body "Session [date]: [what was done]"

# Update body (replace entirely — read first, modify, write back)
gh issue edit {number} --body-file /tmp/updated-body.md
```

### Close when done

```bash
gh issue close {number} --reason completed --comment "Completed in session [date]."
```

### Update tracking issue checklist

When a department issue is closed, update the tracking issue's progress section:
- Change `- [ ] #NNN` to `- [x] #NNN`
- Update status count: "Status: 3/7 complete"

## Slug Convention

The initiative slug is a kebab-case identifier derived from the initiative name:
- "Add referral program" → `impact-referral-program`
- "Fix billing bug" → `impact-billing-bug`
- "P0 Infrastructure Sprint" → `impact-p0-infra`

Used as a label to group all issues for one initiative.

## Execution Loop Commands

When resuming work on an existing initiative:

```bash
# 1. Find open items
gh issue list --label impact-{slug} --state open --json number,title,labels,body

# 2. Check what's unblocked (parse "Blocked By" in body — if all blockers are closed, it's unblocked)
# For each open issue, check if blocking issues are closed:
gh issue view {blocker-number} --json state

# 3. Work the item (or spawn agent)

# 4. Close when done
gh issue close {number} --reason completed --comment "Done."

# 5. Check if tracking issue needs update
gh issue view {tracking-number} --json body
# Update checklist in body
```

## When NOT to Use GitHub Issues

- Single-session tasks (use Claude Code TaskCreate instead)
- Fewer than 3 deliverables (overhead not worth it)
- User explicitly says no
- No `gh` CLI available or not authenticated
