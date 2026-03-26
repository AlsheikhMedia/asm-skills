# Product — Impact Checklist

When a feature, task, or initiative affects the Product team, use this checklist to identify specific deliverables, dependencies, and risks.

## What to Check

### Requirements & Specification
- [ ] Feature spec exists (user stories, acceptance criteria, edge cases)
- [ ] Scope is explicitly bounded (what's IN, what's OUT, what's DEFERRED)
- [ ] Success metrics defined (how do we know this worked?)
- [ ] User flow documented (happy path + error paths)
- [ ] Edge cases enumerated (empty states, limits, concurrent access, permissions)
- [ ] Data model implications reviewed (new entities, changed relationships)

### Launch & Rollout
- [ ] Launch checklist created (all steps from code-complete to live)
- [ ] Rollout strategy defined (big bang, phased, feature-flagged, beta)
- [ ] Kill criteria defined (metrics that trigger rollback or pivot)
- [ ] Rollback plan documented (how to undo if something goes wrong)
- [ ] Internal announcement drafted (team knows what's shipping and why)
- [ ] Release notes drafted (customer-facing changelog)

### Pricing & Packaging
- [ ] Feature placement decided (which plan/tier includes this?)
- [ ] Pricing page update needed?
- [ ] Feature comparison table update needed?
- [ ] Entitlement/gating logic defined (how is access controlled?)
- [ ] Upgrade path clear (how do free users discover this is paid?)

### Documentation & Communication
- [ ] Help docs / knowledge base article written or updated
- [ ] In-app guidance considered (tooltips, onboarding steps, empty states)
- [ ] Internal FAQ for customer-facing teams
- [ ] Demo script updated (if this changes the standard demo)

## Typical Dependencies

**Product needs FROM:**

| Department | What | Why |
|-----------|------|-----|
| Research | ICP validation, pain point confirmation, competitor analysis | Spec needs to solve real problems |
| Finance | Pricing decisions, unit economics validation | Can't spec packaging without pricing |
| Legal | Compliance constraints, data handling requirements | Can't spec features that violate regulations |
| Design/UX | Feasibility feedback, UX research findings | Can't spec interactions without design input |
| Development | Technical constraints, effort estimates, feasibility | Can't spec what can't be built in the timeline |

**Product PRODUCES for:**

| Department | What | Why |
|-----------|------|-----|
| Development | Spec, acceptance criteria, priority, edge case decisions | Dev needs clear requirements |
| Design/UX | Requirements, user flows, content for mockups | Design needs to know what to design |
| QA/Testing | Acceptance criteria, edge cases, test scenarios | QA needs to know what "correct" looks like |
| Content/Marketing | Feature positioning, messaging input, value props | Marketing needs to know what to say |
| Sales | Feature talking points, competitive positioning, demo script | Sales needs to know how to sell it |
| Customer Success | Feature documentation, known limitations, FAQ | CS needs to support it |

## Common Deliverables by Initiative Type

### New Feature
- [ ] Feature spec with acceptance criteria
- [ ] Scoped user stories (prioritized: must/should/could)
- [ ] Data model review sign-off
- [ ] Launch checklist
- [ ] Rollout strategy decision
- [ ] Release notes draft
- [ ] Pricing/packaging decision (if applicable)

### Feature Enhancement
- [ ] Change spec (what's changing, what's not)
- [ ] Migration/backward compatibility decision
- [ ] Updated acceptance criteria
- [ ] Changelog entry

### Infrastructure/Technical Initiative
- [ ] Business case (why now, what's the cost of not doing it)
- [ ] Success criteria (how do we verify it worked)
- [ ] User impact assessment (any downtime, behavior changes?)
- [ ] Communication plan (does anyone outside eng need to know?)

### Campaign / Go-to-Market
- [ ] Campaign brief (goals, audience, channels, timeline)
- [ ] Success metrics + kill criteria
- [ ] Budget allocation (if applicable)
- [ ] Cross-department coordination plan

## Common Mistakes

- Spec is too vague ("allow flexible types" vs. "support these 5 specific type configurations with these behaviors")
- No explicit scope boundaries (scope creep kills timelines)
- Missing edge cases that Development discovers mid-sprint (rework)
- No kill criteria for campaigns or experiments (zombie initiatives)
- Forgetting to update pricing page / feature comparison after launch
- No rollback plan (especially for schema changes or pricing changes)
- Skipping the internal FAQ (CS and Sales get surprised by customer questions)
- Success metrics defined after launch (can't measure what you didn't instrument)
