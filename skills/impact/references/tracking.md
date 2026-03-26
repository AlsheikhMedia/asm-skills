# Task Tracking Reference

How the impact skill tracks deliverables across sessions. Three backends, auto-detected.

## Provider Detection

```
1. git remote get-url origin
2. Match provider:
   - github.com    → GitHub (check: which gh)
   - gitlab.com    → GitLab (check: which glab)
   - codeberg.org  → Codeberg/Forgejo (uses curl + Gitea API)
   - bitbucket.org → Bitbucket (uses curl + Bitbucket API)
   - Other/none    → Local tracking
3. If CLI not found → fall back to local tracking
4. Ask: "Detected [provider]. Track with [provider] issues, or keep it local?"
```

## Slug Convention

Derive a kebab-case slug from the initiative name:
- "Add referral program" → `impact-referral-program`
- "Fix billing bug" → `impact-billing-bug`
- "P0 Infrastructure Sprint" → `impact-p0-infra`

Used as a label/tag to group all tasks for one initiative.

---

## Local Tracking (Universal Default)

File: `.claude/impact-tasks.md` — works everywhere, zero dependencies.

### File Format

```markdown
# Impact: [Initiative Name]

**Created:** [date] | **Status:** 0/[N] complete

## Dependency Chain
Product → Design → Development → QA
                                  ↘ Marketing
                                  ↘ CS

## Tasks

### Phase 1 — Blocking
- [ ] **Product**: Feature spec with acceptance criteria — Unblocked
- [ ] **Design**: Mockups for referral page — Blocked by: Product

### Phase 2 — Parallel
- [ ] **Development**: Schema + API + UI — Blocked by: Design
- [ ] **Legal**: Review referral terms — Unblocked

### Phase 3 — Follow-up
- [ ] **QA**: Journey test + abuse scenarios — Blocked by: Development
- [ ] **Marketing**: Announcement + copy — Blocked by: Development
- [ ] **CS**: Knowledge base article — Blocked by: Development
```

### Operations

**Create**: Write file after impact analysis (Step 6).

**Check progress**: Read file, parse checkboxes. `[x]` = done, `[ ]` = todo.

**Find unblocked**: Parse "Blocked by:" tags. If all blockers are checked `[x]`, the item is unblocked. Items marked "Unblocked" are always ready.

**Mark done**: Change `- [ ]` to `- [x]`, append `— DONE [date]`:
```
- [x] **Product**: Feature spec with acceptance criteria — DONE 2026-03-26
```

**Update status**: Change count in header: "Status: 3/7 complete"

**Detect existing**: On trigger, check if `.claude/impact-tasks.md` exists and has unchecked items.

### When to Use Local

- No git remote or unsupported provider
- User prefers local tracking
- Fewer than 3 deliverables (remote issues are overhead)
- Single-person project (no team visibility needed)

---

## GitHub Issues

Auto-detected when remote contains `github.com` and `gh` CLI is available.

### Label Convention

**Type:** `impact`, `tracking`
**Department:** `dept-product`, `dept-dev`, `dept-qa`, `dept-design`, `dept-marketing`, `dept-devops`, `dept-sales`, `dept-cs`, `dept-legal`, `dept-finance`, `dept-research`, `dept-analytics`, `dept-security`, `dept-brand`
**Priority:** `p0-blocker`, `p1-parallel`, `p2-followup`
**Phase:** `phase-1`, `phase-2`, `phase-3`

### Tracking Issue Template

```markdown
# Impact: [Initiative Name]

**Scope:** [1-line]
**Created:** [date]
**Status:** 0/[N] complete

## Progress
- [ ] #NNN [Department]: [Key deliverable]

## Dependency Chain
[Dept A] (#NNN) → [Dept B] (#NNN) → [Dept C] (#NNN)
```

Labels: `impact`, `impact-{slug}`, `tracking`

### Department Issue Template

```markdown
## [Department] — [Initiative Name]

**Priority:** Blocking / Parallel / Follow-up
**Estimate:** [range] | **Phase:** [1/2/3]

### Deliverables
- [ ] [Specific item]

### Blocked By
- #NNN ([what])

### Unblocks
- #NNN ([what])
```

Labels: `impact`, `impact-{slug}`, `dept-{name}`, `phase-{n}`, priority

### Commands

```bash
# Create
gh issue create --title "Impact: [Name]" --label "impact,impact-{slug},tracking" --body "..."
gh issue create --title "[Dept]: [Deliverable] — [Name]" --label "impact,impact-{slug},dept-{name}" --body "..."

# List open
gh issue list --label impact-{slug} --state open --json number,title,labels

# Close
gh issue close {N} --reason completed --comment "Done."

# Update tracking checklist
gh issue edit {tracking-N} --body "..." # change [ ] to [x], update count
```

---

## GitLab Issues

Auto-detected when remote contains `gitlab.com` or `gitlab.*` and `glab` CLI is available.

### Commands

```bash
# Create
glab issue create --title "[Title]" --label "impact,impact-{slug}" --description "..."

# List
glab issue list --label impact-{slug} --in title

# Close
glab issue close {N}

# Comment
glab issue note {N} --message "Done."
```

Labels and templates: same structure as GitHub.

---

## Codeberg / Forgejo (Gitea API)

Auto-detected when remote contains `codeberg.org` or known Forgejo instances. Uses `curl` with Gitea API.

Requires token: `export CODEBERG_TOKEN="your-token"`

### Commands

```bash
BASE="https://codeberg.org/api/v1"
REPO="{owner}/{repo}"

# Create issue
curl -X POST "$BASE/repos/$REPO/issues" \
  -H "Authorization: token $CODEBERG_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"title": "[Title]", "body": "..."}'

# List open issues
curl "$BASE/repos/$REPO/issues?state=open&labels=impact" \
  -H "Authorization: token $CODEBERG_TOKEN"

# Close issue
curl -X PATCH "$BASE/repos/$REPO/issues/{id}" \
  -H "Authorization: token $CODEBERG_TOKEN" \
  -d '{"state": "closed"}'
```

Note: Labels must be created first via web UI. Use label IDs in create requests.

---

## Bitbucket Issues

Auto-detected when remote contains `bitbucket.org`. Uses Bitbucket API v2.0.

Requires: `export BITBUCKET_USER="user"` and `export BITBUCKET_APP_PASSWORD="password"`

### Commands

```bash
BASE="https://api.bitbucket.org/2.0"
REPO="{workspace}/{repo}"

# Create issue
curl -X POST "$BASE/repositories/$REPO/issues" \
  -u "$BITBUCKET_USER:$BITBUCKET_APP_PASSWORD" \
  -H "Content-Type: application/json" \
  -d '{"title": "[Title]", "content": {"raw": "..."}, "kind": "task"}'

# List open issues
curl "$BASE/repositories/$REPO/issues?q=state=\"open\"" \
  -u "$BITBUCKET_USER:$BITBUCKET_APP_PASSWORD"

# Close issue
curl -X PUT "$BASE/repositories/$REPO/issues/{id}" \
  -u "$BITBUCKET_USER:$BITBUCKET_APP_PASSWORD" \
  -d '{"state": "resolved"}'
```

Note: Bitbucket doesn't support custom labels. Use title prefixes: `[Impact] [Dept] Title`.

---

## When NOT to Use Remote Issues

- Single-session tasks (use Claude Code TaskCreate)
- Fewer than 3 deliverables (use local tracking)
- User explicitly declines
- CLI/API auth not configured
- Always fall back to local — never fail silently
