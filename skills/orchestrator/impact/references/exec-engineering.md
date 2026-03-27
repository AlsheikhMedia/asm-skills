# Engineering — Execution Module

Load this when the impact execution loop needs to build features, fix bugs, refactor code, or handle infrastructure work.

## Modes

**Feature Mode** (default): Build a new feature end-to-end — schema → server → components → pages → tests → deploy.

**Fix Mode**: Fix a bug or issue — reproduce → diagnose → fix → regression test.

**Infrastructure Mode**: Non-UI engineering work — CI/CD, monitoring, migrations, performance.

**Refactor Mode**: Restructure existing code — identify scope → refactor → verify no regressions.

Detect mode from the task description. If ambiguous, default to Feature Mode.

## Step 1: Gather Context

Before writing any code:

1. **Project conventions**: Read `CLAUDE.md`, `.claude/`, design guides, component APIs, style guides
2. **Route structure**: If building UI, read existing routes to understand patterns
3. **Database schema**: If touching data layer, read current schema and migrations
4. **Test patterns**: Read existing tests to understand frameworks, naming, and coverage expectations
5. **Quality gates**: Check for page checklists, UI quality standards, lint configs
6. **Existing state**: If resuming from a checkpoint, read `.claude/impact-tasks.md` for the last completed phase

Do NOT skip context gathering. Building without understanding conventions creates rework.

## Step 2: Plan (Write to File)

Create `.claude/impact-engineering-plan.md` with:

```markdown
# Engineering Plan — [Feature/Task Name]

**Mode:** Feature / Fix / Infrastructure / Refactor
**Date:** [date]

## Files to Create/Modify
- [path] — [purpose]

## Database Changes
- [migration description, or "None"]

## Component Dependencies
- [what depends on what]

## Test Strategy
- Unit: [what to cover]
- Integration: [what to cover]
- E2E: [what to cover, or "N/A"]

## Deployment Considerations
- [staging, feature flags, migration order, or "Standard deploy"]
```

Present the plan to the user. Get confirmation before proceeding.

## Step 3: Implement

Follow this order — dependencies flow downward:

### 3.1 Schema Changes
- Write migrations for new tables, columns, indexes
- Update ORM models and type definitions
- Update seed data
- Run migration locally and verify

### 3.2 Server Logic
- API routes, server loaders, form actions, DB queries
- Input validation and error handling
- Auth guards and rate limiting

### 3.3 Shared Utilities
- Validation schemas (Zod, etc.)
- Type definitions and interfaces
- Helper functions

### 3.4 Components
- Follow project design system (tokens, spacing, typography)
- All states: default, loading, error, empty, disabled
- Accessibility: labels, keyboard nav, contrast, ARIA, RTL
- Touch targets: 48px minimum, 56px primary CTAs

### 3.5 Pages
- Compose components, wire to server data
- Responsive behavior: mobile → tablet → desktop
- SEO metadata if public-facing

### 3.6 Integration
- Connect all pieces end-to-end
- Handle edge cases from the spec
- Verify data flow from schema to UI

At each sub-step:
- Follow project conventions from CLAUDE.md / design guide
- Match existing patterns (check similar implementations)
- Run type checker after each file change

## Step 4: Verify

Quality gates — run in order, fix failures before proceeding:

1. **Type check**: `bun run check` (or project equivalent) — zero errors
2. **Unit tests**: Write tests for new logic. Run full suite. Zero failures.
3. **Integration tests**: Test API endpoints, DB queries, auth flows.
4. **E2E tests**: Write journey tests for new user flows. Run E2E suite.
5. **Lint/format**: Run linter. Fix violations.
6. **Build**: Full production build must succeed.

If any gate fails: fix the issue, re-run from the failing gate. Do not skip gates.

### Mode-Specific Verification

**Fix Mode**: Write a regression test that reproduces the original bug, then verify it passes after the fix.

**Refactor Mode**: Run full test suite before AND after. Diff must show zero behavior changes. Only structural improvements.

**Infrastructure Mode**: Verify in staging if available. Check monitoring/alerting is active for new paths.

## Step 5: Deploy (If Staging Exists)

1. Check for staging config (`wrangler.staging.toml`, staging scripts, CI deploy job)
2. Deploy to staging
3. Verify deployment loads without errors
4. Report staging URL for manual QA

If no staging environment exists, skip and note it.

## Step 6: Checkpoint

After completion, update `.claude/impact-tasks.md`:

1. Mark the engineering task as done: `- [x] **Engineering**: [deliverable] — DONE [date]`
2. Update the Execution State table:
   ```
   | Engineering | Complete | done | [date] |
   ```
3. Note any deferred items or tech debt created
4. Note test counts if relevant

### Cross-Department Triggers

During implementation, you may discover needs from other departments not identified in the original analysis. When this happens:

1. **DO NOT** handle it inline — stay in your lane
2. **Write to the state file** `.claude/impact-tasks.md`:
   ```
   ## Cross-Department Triggers (auto-generated)
   - [ ] TRIGGER: [Engineering Phase 3] needs [Department] — [specific deliverable]
     - Status: pending
     - Paused at: exec-engineering.md, Phase [N], Step [X]
     - Resume after: [Department] delivers [deliverable]
   ```
3. **Update the Execution State table**:
   ```
   | Engineering | Phase 3: Implement | paused (needs [Dept]) | [date] |
   ```
4. **Return control** to the user: "Engineering paused at Phase 3, Step X. Needs [deliverable] from [Department] before continuing."
5. Impact's execution loop (Step 7) will route to the correct department's exec module
6. When resuming: read the state file, find the checkpoint, continue from the paused step

## Principles

**Plan before code.** The plan file is not optional. It's how you get user buy-in and avoid building the wrong thing.

**Convention over invention.** Match existing patterns. A consistent codebase with a slightly imperfect pattern is better than a codebase with five "better" approaches.

**Gates are not optional.** A feature that compiles but fails tests is not done. A feature that passes tests but doesn't build is not done. Run all gates.

**Small steps, frequent verification.** Don't write 500 lines then check if it compiles. Build incrementally: schema → verify → server → verify → UI → verify.
