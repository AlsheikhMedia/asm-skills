# QA/Testing — Impact Checklist

When a feature, task, or initiative affects QA/Testing, use this checklist to identify specific deliverables, dependencies, and risks.

## What to Check

### Test Planning
- [ ] Test scenarios defined (happy path + edge cases)
- [ ] Acceptance criteria from Product are testable (not vague)
- [ ] Regression scope identified (what existing features could break?)
- [ ] Test data requirements defined (seed data, test accounts, states)
- [ ] Test environment requirements (staging, feature flags, third-party sandboxes)

### Test Types Needed
- [ ] Unit tests (business logic, calculations, validations)
- [ ] Integration tests (API endpoints, database queries, auth guards)
- [ ] E2E tests (critical user journeys, auth flows)
- [ ] Visual regression (if UI changes are significant)
- [ ] Performance testing (if load/scale concerns exist)
- [ ] Cross-browser/device testing (if frontend-heavy)
- [ ] Accessibility testing (keyboard nav, screen reader, contrast)
- [ ] Combinatorial/state-machine tests (if feature has enums, statuses, or permission matrices)

### Combinatorial Testing Heuristic
For features with N enum values, M state transitions, or P permission roles, estimate test matrix size:
- **State machine**: N states x M valid transitions = minimum test scenarios
- **Permission matrix**: P roles x A actions = minimum authorization tests
- **Multi-enum**: Product of enum cardinalities for cross-cutting combinations
- Example: 4 job states x 6 transitions x 2 user roles = 48 minimum test scenarios

### CI Integration
- [ ] New tests added to CI pipeline
- [ ] CI pipeline passes with new tests
- [ ] Test execution time still within budget (< 60s unit, < 5min E2E)
- [ ] Flaky test risk assessed (external dependencies, timing)

## Typical Dependencies

**QA/Testing needs FROM:**

| Department | What | Why |
|-----------|------|-----|
| Product | Acceptance criteria, edge case list, expected behavior | Can't test without knowing what "correct" is |
| Development | Testable build, test environment, test data setup | Can't test what isn't built |
| DevOps | Test environment running, feature flags configured | Can't test without a working environment |
| Design/UX | Visual specs for UI verification | Can't validate UI without reference |

**QA/Testing PRODUCES for:**

| Department | What | Why |
|-----------|------|-----|
| Development | Bug reports, regression findings, test coverage gaps | Dev needs to fix before launch |
| Product | Quality assessment, go/no-go recommendation | Product decides whether to ship |
| DevOps | Confidence for production deployment | DevOps needs green light |

## Common Deliverables by Initiative Type

### New Feature
- [ ] Test plan (scenarios, data, environments)
- [ ] Unit tests for business logic
- [ ] Integration tests for API endpoints
- [ ] E2E journey test (core happy path)
- [ ] Bug report with severity classification
- [ ] Go/no-go assessment

### Infrastructure Change
- [ ] Regression test pass (existing features still work)
- [ ] Performance benchmark comparison (before/after)
- [ ] Deployment verification (smoke tests post-deploy)

### Schema/Data Migration
- [ ] Data integrity verification (before/after migration)
- [ ] Rollback test (migration can be reversed)
- [ ] Seed data updated and verified

## Effort Estimation Guide

| Deliverable | Typical Range |
|------------|--------------|
| Test plan (scenarios + data) | 0.5-1 day |
| Unit test suite (per feature) | 1-2 days |
| E2E journey test | 0.5-1 day |
| Full regression pass | 1-2 days |
| Performance test setup | 1-3 days |
| Cross-browser verification | 0.5-1 day |

## Common Mistakes

- Testing only the happy path (edge cases are where bugs live)
- Starting test writing after development is "done" (should overlap)
- No regression plan (new feature works but old feature broke)
- Hardcoded test data (tests break when seed data changes)
- Testing in development environment (config differences cause false passes)
- No accessibility testing (caught by users, not by QA)
- Flaky tests left in CI (erodes trust in the pipeline)
