# Development — Impact Checklist

When a feature, task, or initiative affects the Development team, use this checklist to identify specific deliverables, dependencies, and risks.

## What to Check

### Scope & Architecture
- [ ] Schema changes required (new tables, columns, relations, indexes)
- [ ] API changes required (new endpoints, modified payloads, breaking changes)
- [ ] UI components needed (new pages, modified components, new shared components)
- [ ] State management changes (new stores, modified data flow)
- [ ] Third-party integrations (new SDKs, API connections, webhooks)
- [ ] Migration path for existing data (backfill, transformation, cleanup)
- [ ] Feature flag requirements (gated rollout, A/B testing, per-org control)

### Implementation Considerations
- [ ] Effort estimation provided (in days, with range: optimistic/realistic/pessimistic)
- [ ] Technical constraints documented (performance requirements, backward compatibility)
- [ ] Build order defined (what gets built first, what depends on what)
- [ ] Slicing strategy clear (how is this broken into mergeable increments?)
- [ ] Shared component opportunities identified (reusable across features)
- [ ] Tech debt implications assessed (does this create debt or pay it down?)

### Integration Points
- [ ] API contract agreed with frontend/consumers before implementation starts
- [ ] Database schema reviewed by team before migration is written
- [ ] Breaking changes communicated to all affected consumers
- [ ] Backward compatibility strategy defined (if serving existing clients)

## Typical Dependencies

**Development needs FROM:**

| Department | What | Why |
|-----------|------|-----|
| Product | Spec/requirements, acceptance criteria, edge case decisions | Can't build what isn't defined |
| Design/UX | Mockups, component specs, interaction patterns | Can't build UI without design |
| DevOps | Environment setup, CI pipeline, deployment config | Can't deploy without infrastructure |
| Legal | Data handling requirements, compliance constraints | Can't design schema without knowing what data rules apply |
| Finance | Pricing logic, billing integration requirements | Can't implement what isn't decided |

**Development PRODUCES for:**

| Department | What | Why |
|-----------|------|-----|
| QA/Testing | Testable build, test environment, test data setup | QA can't test what isn't built |
| DevOps | Deployment artifacts, environment requirements, config changes | DevOps can't deploy what isn't ready |
| Analytics | Tracking event implementations, data layer changes | Analytics can't measure what isn't instrumented |
| Content/Marketing | Feature screenshots, accurate capability descriptions | Marketing can't promote what doesn't exist |
| Customer Success | Feature documentation input, known limitations | CS can't support what they don't understand |
| Design/UX | Implementation feedback, feasibility constraints | Design needs to know what's possible |

## Common Deliverables by Feature Type

### Schema Change
- [ ] Migration file (reviewed before running)
- [ ] Updated ORM models/types
- [ ] Seed data updated for new schema
- [ ] Rollback strategy documented

### New API Endpoint
- [ ] Endpoint implementation with validation
- [ ] Auth guard applied
- [ ] Rate limiting configured
- [ ] API documentation updated
- [ ] Error responses defined

### New UI Feature
- [ ] Page/component implementation
- [ ] Loading/error/empty states
- [ ] Responsive behavior (mobile, tablet, desktop)
- [ ] Accessibility (labels, keyboard nav, contrast)
- [ ] Route protection (auth guards)

### Landing Page / Marketing Page
- [ ] OG images and social sharing metadata (title, description, image)
- [ ] Twitter/X card meta tags
- [ ] Analytics pixels and tracking events (page view, form submit, CTA click)
- [ ] Performance budget (above-fold load time < 1.5s for campaign pages)
- [ ] UTM parameter handling (capture and store for attribution)
- [ ] Form validation and submission flow
- [ ] Confirmation/thank-you page or state

### Feature Flag Gated Launch
- [ ] Flag defined in flag system
- [ ] Code paths for flag on/off
- [ ] Cleanup plan documented (when to remove flag)
- [ ] Admin ability to toggle per-org

## Effort Estimation Guide

| Scope | Typical Range | Includes |
|-------|--------------|----------|
| Schema change only | 0.5-1 day | Migration + model update + seed update. Multiply by number of related tables for complex schema changes. |
| Single API endpoint | 0.5-2 days | Implementation + validation + tests |
| Single page/component | 1-3 days | UI + states + responsive + accessibility |
| Full feature (schema + API + UI) | 3-10 days | All of the above + integration |
| Multi-slice feature | 1-4 weeks | Multiple increments, each independently deployable |
| Infrastructure change | 1-5 days | Config + testing + rollout + monitoring |

These are work time only. Add dependency wait time separately.

## Common Mistakes

- Starting implementation before schema is agreed (leads to rework)
- Building the entire feature before deploying anything (delays feedback)
- Not defining the slicing strategy upfront (monolithic PRs that are hard to review)
- Skipping feature flags for user-facing changes (all-or-nothing launch)
- Not communicating API contract changes to consumers early
- Estimating only the happy path (edge cases and error handling take 30-50% of effort)
- Forgetting to update seed data (demo environment breaks)
