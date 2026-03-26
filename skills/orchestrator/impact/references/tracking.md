# Task Tracking Reference

## Local Tracking

File: `.claude/impact-tasks.md`

```markdown
# Impact: [Initiative Name]

**Created:** [date] | **Status:** 0/[N] complete

## Dependency Chain
[Dept A] → [Dept B] → [Dept C]
                        ↘ [Dept D] (parallel)

## Tasks

### Phase 1 — Blocking
- [ ] **[Department]**: [Deliverable] — Unblocked
- [ ] **[Department]**: [Deliverable] — Blocked by: [Department]

### Phase 2 — Parallel
- [ ] **[Department]**: [Deliverable] — Blocked by: [Department]

### Phase 3 — Follow-up
- [ ] **[Department]**: [Deliverable] — Blocked by: [Department]
```

Mark done: `- [x] **Product**: Feature spec — DONE 2026-03-26`

---

## Remote Issue Templates (All Providers)

### Tracking Issue (Epic)

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

### Department Issue

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

### Label Convention

- **Type:** `impact`, `tracking`
- **Department:** `dept-product`, `dept-dev`, `dept-qa`, `dept-design`, `dept-marketing`, `dept-devops`, `dept-sales`, `dept-cs`, `dept-legal`, `dept-finance`, `dept-research`, `dept-analytics`, `dept-security`, `dept-brand`
- **Priority:** `p0-blocker`, `p1-parallel`, `p2-followup`
- **Phase:** `phase-1`, `phase-2`, `phase-3`

---

## Provider-Specific Commands

### GitHub (`gh` CLI)

```bash
gh issue create --title "[Title]" --label "impact,impact-{slug},dept-{name}" --body "..."
gh issue list --label impact-{slug} --state open --json number,title,labels
gh issue close {N} --reason completed --comment "Done."
```

### GitLab (`glab` CLI)

```bash
glab issue create --title "[Title]" --label "impact,impact-{slug}" --description "..."
glab issue list --label impact-{slug}
glab issue close {N}
```

### Codeberg / Forgejo (Gitea API)

Requires: `export CODEBERG_TOKEN="your-token"`

```bash
BASE="https://codeberg.org/api/v1"
REPO="{owner}/{repo}"

curl -X POST "$BASE/repos/$REPO/issues" \
  -H "Authorization: token $CODEBERG_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"title": "[Title]", "body": "..."}'

curl "$BASE/repos/$REPO/issues?state=open&labels=impact" \
  -H "Authorization: token $CODEBERG_TOKEN"

curl -X PATCH "$BASE/repos/$REPO/issues/{id}" \
  -H "Authorization: token $CODEBERG_TOKEN" \
  -d '{"state": "closed"}'
```

Labels must be created via web UI first.

### Bitbucket (API v2.0)

Requires: `export BITBUCKET_USER="user"` and `export BITBUCKET_APP_PASSWORD="password"`

```bash
BASE="https://api.bitbucket.org/2.0"
REPO="{workspace}/{repo}"

curl -X POST "$BASE/repositories/$REPO/issues" \
  -u "$BITBUCKET_USER:$BITBUCKET_APP_PASSWORD" \
  -H "Content-Type: application/json" \
  -d '{"title": "[Impact][Dept] Title", "content": {"raw": "..."}, "kind": "task"}'

curl "$BASE/repositories/$REPO/issues?q=state=\"open\"" \
  -u "$BITBUCKET_USER:$BITBUCKET_APP_PASSWORD"

curl -X PUT "$BASE/repositories/$REPO/issues/{id}" \
  -u "$BITBUCKET_USER:$BITBUCKET_APP_PASSWORD" \
  -d '{"state": "resolved"}'
```

No custom labels — use title prefixes: `[Impact] [Dept] Title`.
