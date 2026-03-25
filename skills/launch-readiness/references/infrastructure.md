# Infrastructure Checklist

## Error Monitoring {#error-monitoring}

Error monitoring is the first thing to set up because without it, you're flying blind. Every bug that hits production is invisible until a customer complains.

### What to Check

- [ ] Error tracking SDK installed and initialized (client + server)
- [ ] Source maps uploaded (stack traces show real file/line, not minified garbage)
- [ ] Environment tagging (development vs staging vs production)
- [ ] Sample rate configured (not 100% in production — 10-20% for transactions, 100% for errors)
- [ ] Unhandled promise rejections captured
- [ ] Server-side errors captured (not just console.log)
- [ ] Alert rules configured (email/Slack on new error types or spike)
- [ ] CSP updated to allow error reporting domain

### Framework-Specific

**SvelteKit:**

- `@sentry/sveltekit` (or equivalent) installed
- `hooks.server.ts` → `handleError` wraps Sentry
- `hooks.client.ts` → client-side Sentry init + `handleError`
- `vite.config.ts` → `sentrySvelteKit()` plugin for source maps
- CSP in `svelte.config.js` updated for Sentry domain in `connect-src`

**Next.js:**

- `@sentry/nextjs` installed
- `sentry.server.config.ts` + `sentry.client.config.ts` + `sentry.edge.config.ts`
- `next.config.js` → `withSentryConfig()` wrapper
- `instrumentation.ts` for server-side init (App Router)

**Nuxt:**

- `@sentry/nuxt` or `nuxt-sentry` module
- Plugin in `plugins/sentry.client.ts`
- Server middleware for server-side errors

### Common Mistakes

- Forgetting client-side error capture (only wiring server)
- Not uploading source maps (stack traces are useless without them)
- Setting 100% sample rate in production (costs money, slows requests)
- Not adding the error tracking domain to CSP (errors silently fail to report)

---

## CI/CD Pipeline {#ci-cd}

CI is a pre-deploy gate. If it doesn't pass, code doesn't ship. The goal is catching problems before they reach production.

### What to Check

- [ ] Pipeline runs on every push to main AND every PR
- [ ] Steps in order: type-check → lint → test → build
- [ ] PR merge blocked if any step fails
- [ ] Security scanning (dependency vulnerabilities, secrets detection, SAST)
- [ ] Build artifacts cached (faster runs)
- [ ] Status badge in README
- [ ] Pipeline runs in < 10 minutes (otherwise developers bypass it)

### Minimum Pipeline

```yaml
# This is the minimum viable CI — adapt to your platform
jobs:
  check:
    steps:
      - Type check (tsc --noEmit / svelte-check / nuxt typecheck)
      - Lint (eslint / biome)
  test:
    needs: check
    steps:
      - Unit + integration tests
  build:
    needs: test
    steps:
      - Production build (verify it compiles)
  security:
    # Runs in parallel, advisory
    steps:
      - Dependency vulnerability scan (trivy / npm audit / snyk)
      - Secrets detection (gitleaks / truffleHog)
      - Static analysis (semgrep / eslint-plugin-security)
```

### What NOT to Put in CI (Yet)

- E2E tests (too slow for every PR — run nightly or on staging deploy)
- Performance benchmarks (separate scheduled job)
- Production deployment (separate workflow, manual trigger or on merge to main)

---

## Database Migrations {#migrations}

Migrations are version-controlled schema changes. They exist so you never run raw SQL against production and can always reproduce the exact schema state.

### What to Check

- [ ] ORM with migration support configured (Drizzle, Prisma, Knex, TypeORM, etc.)
- [ ] Migration files versioned in git (not gitignored)
- [ ] Migration runner script exists (one command to apply pending migrations)
- [ ] Migration runner exits with code 1 on failure (for CI integration)
- [ ] Schema and migrations are in the same repo (not managed through a dashboard)
- [ ] Migration workflow documented (generate → review → commit → apply)
- [ ] Existing migration files are never edited or deleted
- [ ] Rollback strategy documented (even if it's "restore from backup")

### Migration Runner Pattern

The runner should:

1. Read DATABASE_URL from environment
2. Exit with helpful message if DATABASE_URL is missing
3. Apply all pending migrations in order
4. Log each migration applied
5. Exit 0 on success, 1 on failure

### Framework-Specific

**Drizzle ORM:**

```
drizzle-kit generate  → creates SQL migration files
drizzle-kit migrate   → applies pending migrations
drizzle-kit push      → pushes schema directly (dev only, skip in prod)
```

**Prisma:**

```
prisma migrate dev    → create + apply (development)
prisma migrate deploy → apply only (production)
```

### Common Mistakes

- Using `db push` or `prisma db push` in production (bypasses migration history)
- Editing existing migration files (breaks the migration chain)
- Not reviewing generated SQL before committing (auto-generated migrations can be destructive)
- Running migrations as part of the app startup (should be a separate deploy step)

---

## Staging Environment {#staging}

Staging is your last chance to catch problems before production. If you don't have staging, you're testing in production.

### What to Check

- [ ] Separate environment exists (different URL, different database)
- [ ] Environment variables separated (.env.staging vs .env.production)
- [ ] Deploy to staging before production — always (workflow enforced, not just convention)
- [ ] Staging data is realistic (seeded, not empty)
- [ ] Staging uses same infrastructure as production (same hosting, same DB provider)
- [ ] Staging URL documented and accessible to the team
- [ ] Deploy scripts exist for both staging and production

### Environment Separation

At minimum, these must be different between staging and production:

- Database connection string
- Auth provider project/tenant
- API keys (use test/sandbox keys in staging)
- App URL (staging.app.example.com vs app.example.com)
- Error monitoring environment tag

These can be the same:

- Hosting platform
- Error monitoring DSN (use environment tags to separate)
- CDN configuration

### Deploy Flow

```
PR → CI passes → merge to main → auto-deploy to staging → manual QA → promote to production
```

Or for smaller teams:

```
PR → CI passes → deploy preview (per-PR staging) → merge → auto-deploy to production
```

---

## Seed Data & Demo Environment {#seed-data}

A seed script creates realistic test data so developers aren't working against empty databases and demos aren't embarrassing.

### What to Check

- [ ] Seed script exists (one command: `npm run seed` / `bun run seed`)
- [ ] Script is idempotent (safe to re-run without duplicating data)
- [ ] Data is realistic (real-looking names, addresses, dates — not "test123")
- [ ] Data covers all entity types in the schema
- [ ] Data includes various states (active, pending, completed, failed, archived)
- [ ] Data includes edge cases (empty lists, long names, special characters)
- [ ] Script requires DATABASE_URL (fails gracefully without it)
- [ ] Data matches locale (if the app is for a specific market, use that locale's data)

### What Good Seed Data Looks Like

For a B2B SaaS, a seed script should create:

- 1-2 organizations with different subscription tiers
- 5-15 users across different roles
- Realistic business data (enough to fill tables, charts, dashboards)
- Date ranges that include recent data (not all from 2020)
- Some data in "problem" states (overdue, failed, escalated) so error handling is visible

### Idempotency Strategies

- **Deterministic IDs**: Use UUID v5 with a namespace so the same entities always get the same IDs
- **Check before insert**: `SELECT` first, skip if exists
- **ON CONFLICT DO NOTHING**: Let the DB handle duplicates
- **Truncate + reseed**: Wipe and recreate (simpler, but loses any manual test data)

---

## Security Baseline {#security}

Security isn't a feature — it's a prerequisite. These are the minimum items that should be in place before any user touches the app.

### What to Check

- [ ] Security headers set (X-Frame-Options, X-Content-Type-Options, HSTS, Referrer-Policy, Permissions-Policy)
- [ ] CSP (Content Security Policy) configured and not set to `*`
- [ ] CORS not set to wildcard `*` on API endpoints
- [ ] Auth guards on all protected routes (not just frontend redirects — server-side enforcement)
- [ ] Rate limiting on auth endpoints (login, signup, password reset)
- [ ] Rate limiting on API endpoints
- [ ] No secrets in git history (run gitleaks/truffleHog)
- [ ] Environment variables for all secrets (not hardcoded)
- [ ] Session cookies: httpOnly, secure, sameSite
- [ ] Error messages don't leak stack traces in production
- [ ] File upload validation (if applicable): type, size, filename sanitization

### Framework-Specific

**SvelteKit:**

- Security headers in `hooks.server.ts` handle function
- Auth guard in `hooks.server.ts` (check session before route resolution)
- CSP in `svelte.config.js`
- Rate limiting middleware (custom or library)

**Next.js:**

- Security headers in `next.config.js` or `middleware.ts`
- Auth in middleware.ts (runs on edge)
- CSP via meta tag or headers

---

## Feature Flags {#feature-flags}

Feature flags let you ship code without shipping features. They decouple deployment from release and let you test with specific users/orgs before going wide.

### What to Check

- [ ] Feature flag system exists (table/service + utility function)
- [ ] `isFeatureEnabled(key, context)` utility available server-side
- [ ] Flags can be toggled without redeployment
- [ ] Admin UI to manage flags (or at minimum, a CLI/API)
- [ ] Per-org or per-user overrides supported
- [ ] Default values defined (flag missing = feature off)

### When to Implement

Feature flags are P2 — not needed for initial launch. Implement when:

- You have multiple customers and need to roll out features gradually
- You want to A/B test functionality
- You have a sales team that promises features to specific customers

### Minimum Viable Implementation

```
1. Database table: feature_flags (key, enabled, description, created_at)
2. Utility: isFeatureEnabled(key, orgId?) → boolean
3. Admin page: list flags with toggle switches
4. Optional: org_feature_overrides table for per-org control
```

Don't over-engineer this. A database table + utility function is enough to start. You can add LaunchDarkly/Flagsmith/PostHog later if needed.
