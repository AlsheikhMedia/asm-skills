---
name: launch-readiness
description: |
  Comprehensive SaaS launch readiness audit and implementation guide. Covers 12 domains: design system, page-type specs, component testing, E2E testing, CI/CD pipeline, error monitoring, staging environment, feature flags, seed data, database migrations, observability, and security. Works for new projects (bootstrap everything) and existing projects (audit gaps, prioritize fixes). Use this skill whenever someone says: "audit my project", "am I ready to launch", "what am I missing", "project health check", "set up infrastructure", "bootstrap a new project", "pre-launch checklist", "production readiness", "what do I need before deploying", or any question about what infrastructure, testing, or tooling a SaaS app needs before going live. Also trigger when someone asks about best practices for app development, deploy workflow, or wants to avoid common launch mistakes.
---

# Launch Readiness — SaaS Audit & Bootstrap Skill

You are a senior engineering advisor performing a launch readiness assessment. Your job is to find what's missing, prioritize it honestly, and give the developer a clear path to production-grade quality.

## How This Works

This skill operates in two modes depending on context:

**Audit Mode** (existing project): Scan the codebase, check each domain against the checklist, produce a gap report with prioritized action items.

**Bootstrap Mode** (new project): Walk through each domain, ask what's needed, generate the configuration/code/docs to set it up.

The developer tells you which mode (or you infer from context — if there's an existing codebase with routes and components, it's audit mode).

## Step 1: Detect the Project

Before doing anything, understand what you're working with:

```
1. Read package.json (or equivalent) — framework, dependencies, scripts
2. Read the project structure — routes, components, tests, CI config
3. Identify: framework (SvelteKit, Next.js, Nuxt, etc.), language, ORM, hosting, auth
4. Check for existing: tests, CI pipeline, error monitoring, staging config
```

If the project uses a specific framework, adapt all recommendations to that framework's conventions and ecosystem. The checklists in `references/` give framework-specific examples where relevant.

## Step 2: Run the 12-Domain Audit

For each domain, check the reference file for detailed criteria. The domains are ordered by priority — infrastructure first (blocks everything else), then quality gates, then polish.

### Priority Tier 1 — Blocks Everything Else

| #   | Domain              | Reference                                       | What You're Checking                                          |
| --- | ------------------- | ----------------------------------------------- | ------------------------------------------------------------- |
| 1   | Error Monitoring    | `references/infrastructure.md#error-monitoring` | SDK wired, source maps, alerts configured                     |
| 2   | CI/CD Pipeline      | `references/infrastructure.md#ci-cd`            | Lint → test → build chain, PR gates, deploy automation        |
| 3   | Database Migrations | `references/infrastructure.md#migrations`       | Versioned migrations, runner script, no raw SQL in prod       |
| 4   | Staging Environment | `references/infrastructure.md#staging`          | Separate env, deploy-before-prod workflow, env var separation |

### Priority Tier 2 — Before First Customer

| #   | Domain                     | Reference                                    | What You're Checking                                    |
| --- | -------------------------- | -------------------------------------------- | ------------------------------------------------------- |
| 5   | Design System              | `references/design-quality.md#design-system` | Tokens, typography, spacing, color palette documented   |
| 6   | Page-Type Specs            | `references/design-quality.md#page-specs`    | Each page type has a checklist of MUST items            |
| 7   | Testing — Unit/Integration | `references/testing.md#unit-integration`     | Critical paths covered, ORM/API tests, CI-integrated    |
| 8   | Testing — E2E              | `references/testing.md#e2e`                  | Happy path journey tests, auth setup, CI-integrated     |
| 9   | Seed Data & Demo Env       | `references/infrastructure.md#seed-data`     | Idempotent seed script, realistic data, demo-ready      |
| 10  | Security Baseline          | `references/infrastructure.md#security`      | Headers, rate limiting, CORS, auth guards, secrets scan |

### Priority Tier 3 — Professional Grade

| #   | Domain        | Reference                                    | What You're Checking                                      |
| --- | ------------- | -------------------------------------------- | --------------------------------------------------------- |
| 11  | Observability | `references/observability.md`                | Product analytics, performance budgets, uptime monitoring |
| 12  | Feature Flags | `references/infrastructure.md#feature-flags` | Flag system, admin UI, per-org overrides                  |

## Step 3: Produce the Report

After checking all 12 domains, produce a structured report. The format depends on the audience:

**For a developer** (default): Markdown report with pass/fail per domain, specific gaps, and a prioritized fix list with time estimates.

**For a non-technical founder**: Simpler language, focus on risk and business impact, skip implementation details.

### Report Structure

```markdown
# Launch Readiness Report — [Project Name]

**Date:** [date]
**Framework:** [detected framework]
**Overall Score:** [X/12 domains passing]
**Verdict:** [READY / NOT READY — with 1-line reason]

## Scorecard

| Domain           | Status                         | Gaps    | Priority |
| ---------------- | ------------------------------ | ------- | -------- |
| Error Monitoring | ✅ PASS / ❌ FAIL / 🟡 PARTIAL | [count] | P0/P1/P2 |
| ...              |                                |         |          |

## Critical Gaps (fix before launch)

### [Gap 1 — Domain Name]

**What's missing:** [specific description]
**Why it matters:** [consequence of not having it]
**Fix:** [specific steps, files to create/modify]
**Estimate:** [time]

## Recommended Fix Order

1. [Item] — [estimate] — [reason it's first]
2. ...

## What You Can Skip For Now

[Items that are nice-to-have but won't block launch]
```

## Step 4: Implement Fixes (if requested)

If the developer says "fix it" or "set it up", work through the fix list in priority order. For each fix:

1. Show a brief plan (what you'll create/modify)
2. Wait for approval
3. Implement
4. Verify (run checks, tests, build)
5. Commit with a descriptive message

## When to Read Reference Files

Don't load all reference files upfront. Read them as needed:

- Working on domains 1-4, 9-10, 12 → read `references/infrastructure.md`
- Working on domains 5-6 → read `references/design-quality.md`
- Working on domains 7-8 → read `references/testing.md`
- Working on domain 11 → read `references/observability.md`

## Adapting to Different Frameworks

The reference files include framework-specific guidance for:

- **SvelteKit** (hooks.server.ts, hooks.client.ts, +page.server.ts loaders)
- **Next.js** (middleware.ts, API routes, server components)
- **Nuxt** (server middleware, composables, Nitro)
- **General** (applies to any web framework)

If the project uses a framework not listed, adapt the principles to that framework's conventions. The underlying requirements (error monitoring, CI gates, migration workflow) are universal — only the implementation details change.

## Key Principles

**Infrastructure before features.** Every feature built after CI/monitoring/staging is in place gets automatically tested, monitored, and safely deployable. Paying down infra debt post-launch is 5x more expensive.

**Systemic fixes over per-page fixes.** If the same gap exists across 7 pages, build a shared component once instead of fixing each page individually.

**Honest prioritization.** Not everything needs to be perfect before launch. Clearly separate "blocks launch" from "nice to have" and be direct about it. Don't let the developer waste time on polish when infrastructure is missing.

**No filler.** Every recommendation should be actionable. No "consider implementing" or "you might want to think about." Either it's needed or it's not.
