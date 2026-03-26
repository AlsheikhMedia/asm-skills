# Testing Checklist

Testing exists to catch regressions before your customers do. The goal isn't 100% coverage — it's covering the paths that matter most with the least maintenance overhead.

## Unit & Integration Tests {#unit-integration}

### What to Check

- [ ] Test runner configured and working (Vitest, Jest, Mocha, etc.)
- [ ] Test command in package.json (`npm test` / `bun run test`)
- [ ] Tests run in CI pipeline (not just locally)
- [ ] CI fails if tests fail (not advisory — blocking)
- [ ] Critical business logic has tests (calculations, validations, transformations)
- [ ] Database queries/ORM layer has tests (schema validation, query correctness)
- [ ] API/server endpoints have tests (auth guards, input validation, response shapes)
- [ ] Tests use realistic data (not `test123` and `foo@bar.com`)
- [ ] Tests are deterministic (no random failures, no dependency on external services)
- [ ] Test execution time < 60 seconds (otherwise developers stop running them)

### What to Test First (highest ROI)

Priority order for a SaaS app:

1. **Auth logic** — login, signup, session validation, role checks, permission guards
2. **Data validation** — form schemas, API input validation, business rule enforcement
3. **Business calculations** — pricing, scoring, scheduling, aggregations
4. **Database operations** — CRUD operations, complex queries, cascading effects
5. **Utility functions** — formatters, parsers, converters

### What NOT to Test (low ROI)

- UI component rendering (use E2E for this)
- Third-party library behavior (trust the library maintainer)
- Simple getters/setters with no logic
- CSS/styling (visual regression tests are better)

### Test Organization

```
src/
├── lib/
│   ├── server/
│   │   ├── db/
│   │   │   ├── schema.ts
│   │   │   └── __tests__/
│   │   │       ├── schema.test.ts      ← Schema validation
│   │   │       └── queries.test.ts     ← Query correctness
│   │   ├── auth/
│   │   │   └── __tests__/
│   │   │       └── permissions.test.ts ← Role/permission logic
│   │   └── services/
│   │       └── __tests__/
│   │           └── billing.test.ts     ← Business logic
│   └── utils/
│       └── __tests__/
│           └── formatters.test.ts      ← Pure functions
```

Co-locate tests with the code they test. Don't create a separate `/tests/unit/` tree that mirrors the source — it gets out of sync.

---

## E2E Tests {#e2e}

E2E tests verify that the full application works from the user's perspective. They catch integration issues that unit tests miss — broken routes, auth flows that don't redirect properly, forms that submit but don't save.

### What to Check

- [ ] E2E framework configured (Playwright recommended — cross-browser, fast, reliable)
- [ ] E2E command in package.json (`npm run test:e2e`)
- [ ] Dev server auto-starts for E2E runs (Playwright `webServer` config)
- [ ] Auth setup for tests (stored auth state or test credentials)
- [ ] Happy path journey test exists (the core user workflow end-to-end)
- [ ] Auth guard tests exist (unauthenticated users redirected to login)
- [ ] Mobile viewport tests exist (responsive issues caught automatically)
- [ ] Tests don't hardcode IDs or data (navigate from lists, use dynamic selectors)
- [ ] Console errors captured and asserted (no unhandled errors during navigation)
- [ ] Tests run in CI (nightly or on staging deploy — too slow for every PR)

### The Minimum E2E Test Suite

You need exactly these test files to start:

**1. Smoke tests** — Does it load?

- Homepage returns 200
- Login page loads
- CSS/fonts load
- No console errors on page load

**2. Auth tests** — Do guards work?

- Protected routes redirect to login when unauthenticated
- Public routes remain accessible
- Login flow works (if test credentials available)

**3. Journey test** — Does the core workflow work?
The single most important E2E test. For a SaaS app, this is typically:

```
Login → Navigate to main feature → Create entity → Edit entity →
View entity → Verify data persisted → Logout
```

This one test catches 80% of integration bugs.

**4. Responsive tests** — Does mobile work?

- Key pages render at 375px without horizontal overflow
- Navigation is accessible on mobile
- Critical actions are reachable

### Auth in E2E Tests

The biggest blocker for E2E tests is authentication. Three strategies:

**Strategy A: Stored auth state (recommended)**

```typescript
// Setup: login once, save cookies/localStorage
// global-setup.ts
const browser = await chromium.launch();
const page = await browser.newPage();
await page.goto("/login");
await page.fill('input[name="email"]', process.env.TEST_USER_EMAIL);
await page.fill('input[name="password"]', process.env.TEST_USER_PASSWORD);
await page.click('button[type="submit"]');
await page.context().storageState({ path: "auth.json" });
```

**Strategy B: Dev mode bypass**
Many frameworks support a "dev user" that bypasses auth when environment variables aren't set. Tests run in this mode for speed.

**Strategy C: API-based auth**
Hit the auth API directly to get a session token, inject it into the browser context. Fastest, but tightly coupled to auth implementation.

### Test File Organization

```
e2e/
├── smoke.spec.ts              ← Does it load?
├── auth.spec.ts               ← Do guards work?
├── journey-provider.spec.ts   ← Core provider workflow
├── journey-client.spec.ts     ← Core client workflow
├── responsive.spec.ts         ← Mobile viewport checks
└── helpers/
    └── utils.ts               ← Shared helpers (login, navigation)
```

### Page-Type Compliance Tests (Advanced)

Once you have page-type specifications (design checklists), you can write E2E tests that verify every page meets its type's requirements:

- **List pages**: search works, filters persist in URL, pagination works, row click navigates, empty state shown
- **Detail pages**: breadcrumbs visible, tabs sync with URL hash, contact links are `<a>` tags not plain text, status change shows confirmation dialog
- **Dashboards**: KPI cards visible, greeting is time-aware, time range selector works, "View all" links navigate correctly

These tests act as a permanent regression gate — if someone removes a breadcrumb or breaks a filter, CI catches it.

### Common E2E Mistakes

- **Hardcoding element text**: Use `data-testid` or ARIA roles instead of `getByText('Submit')` — text changes break tests
- **`sleep()` instead of waitFor**: Always wait for a specific condition, never a fixed delay
- **Testing implementation details**: Test what the user sees, not internal state
- **Flaky selectors**: Prefer `role` and `testid` over CSS classes (classes change during refactors)
- **No cleanup**: Tests should be independent — don't rely on data from a previous test
