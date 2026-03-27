# Product — Execution Module

Load this when the impact execution loop needs to produce product specs, PRDs, feature requirements, or launch checklists.

## Modes

**Feature Spec** (default): Full PRD with problem statement, user stories, acceptance criteria, edge cases, and success metrics. Use when the task is "write a spec", "PRD", "feature requirements."

**Quick Spec**: Lightweight 1-page spec for small features — what, why, scope, acceptance criteria. Use when the task is small (< 3 days of work) or the user says "quick spec."

**Launch Checklist**: Pre-launch verification list confirming all departments are ready. Use when the task is "launch checklist", "ready to ship?", or "go/no-go."

If uncertain, default to Feature Spec and offer to trim.

## Step 1: Gather Context

Before writing any spec:

1. **Existing features**: Scan routes, pages, and components to understand current product surface
2. **Schema and data model**: Read database schema to understand entities and relationships
3. **User flows**: Trace existing user journeys (signup, onboarding, core actions)
4. **Product-marketing context**: Check for `.claude/product-marketing-context.md` — extract ICP, positioning, business model
5. **Prior specs**: Check for existing specs in `docs/`, `.claude/`, or project wiki references
6. **Constraints**: Timeline, team size, technical limitations from CLAUDE.md or user input

## Step 2: Draft the Spec

### Feature Spec Format

Write to `.claude/impact-spec-[feature-slug].md`:

```markdown
# Feature Spec — [Feature Name]

**Date:** [date] | **Author:** Impact (AI-generated, requires review)
**Status:** Draft

## Problem Statement
[What problem does this solve? Who has this problem? How do we know?]

## Proposed Solution
[High-level description — what the feature does, not how it's built]

## User Stories
- As a [role], I want to [action] so that [outcome]

## Scope

### In Scope
- [Specific deliverable]

### Out of Scope
- [Explicitly excluded item] — [reason]

### Deferred
- [Item for future iteration] — [why not now]

## User Flow
1. [Step] → [Step] → [Step]
   - Error path: [what happens when X fails]
   - Edge case: [unusual but valid scenario]

## Acceptance Criteria
- [ ] [Testable criterion — specific, measurable, not vague]
- [ ] [Another criterion]

## Edge Cases
| Scenario | Expected Behavior |
|----------|------------------|

## Success Metrics
| Metric | Current Baseline | Target | Measurement Method |
|--------|-----------------|--------|-------------------|

## Dependencies
| Department | What's Needed | Blocking? |
|------------|--------------|-----------|

## Open Questions
- [Decision that needs to be made before implementation]
```

### Quick Spec Format

Write to `.claude/impact-spec-[feature-slug].md`:

```markdown
# Quick Spec — [Feature Name]

**Date:** [date] | **Effort:** [estimate]

## What
[1-2 sentences: what are we building?]

## Why
[1-2 sentences: what problem does it solve?]

## Scope
**In:** [bullet list]
**Out:** [bullet list]

## Acceptance Criteria
- [ ] [Criterion]

## Dependencies
- [Department]: [what's needed]
```

### Launch Checklist Format

Write to `.claude/impact-launch-checklist-[feature-slug].md`:

```markdown
# Launch Checklist — [Feature Name]

**Target date:** [date] | **Status:** NOT READY / READY

## Department Sign-off
| Department | Ready? | Blocker | Owner |
|------------|--------|---------|-------|
| Product | [ ] | Spec finalized | |
| Engineering | [ ] | Code complete, tests passing | |
| Design | [ ] | All states designed, reviewed | |
| QA | [ ] | Test pass, no P0/P1 bugs | |
| Marketing | [ ] | Announcement ready | |
| Ops | [ ] | Legal, support, monitoring ready | |

## Pre-Launch
- [ ] Feature flag enabled in staging
- [ ] Staging verified by product + QA
- [ ] Release notes drafted
- [ ] Support team briefed
- [ ] Monitoring/alerting configured

## Launch Day
- [ ] Feature flag enabled in production
- [ ] Smoke test production
- [ ] Announcement published
- [ ] Monitor error rates for 2 hours post-launch

## Post-Launch (Day 1-7)
- [ ] Check success metrics vs. targets
- [ ] Review support tickets for new issues
- [ ] Collect user feedback
- [ ] Decide: iterate, expand, or move on
```

## Step 3: Validate the Spec

Before presenting to the user, verify:

1. **Acceptance criteria are testable**: "Users can export data" is vague. "Users can export their data as CSV from Settings → Export, file downloads within 10 seconds for accounts with < 10k records" is testable.
2. **Scope boundaries are explicit**: Every "In Scope" item has a clear deliverable. "Out of Scope" explains why, not just what.
3. **Success metrics have baselines**: "Increase activation" means nothing without "Activation is currently 23%, target 35%."
4. **Dependencies are specific**: "Needs Design" → "Needs Design: page mockup for referral dashboard, component spec for share widget."
5. **Edge cases cover the non-obvious**: Empty states, permission boundaries, concurrent access, data limits, international/RTL.

## Step 4: Checkpoint

After the spec is written:

1. Mark the product task as done in `.claude/impact-tasks.md`
2. Update the Execution State table:
   ```
   | Product | Spec complete | done | [date] |
   ```
3. Note any open questions that block other departments
4. List cross-department triggers if the spec revealed new dependencies

### Cross-Department Triggers

If writing the spec reveals dependencies not in the original analysis:

1. Write to `.claude/impact-tasks.md`:
   ```
   ## Cross-Department Triggers (auto-generated)
   - [ ] TRIGGER: [Product Spec] needs [Department] — [specific deliverable]
     - Status: pending
     - Paused at: exec-product.md, Step 2
     - Resume after: [Department] delivers [deliverable]
   ```
2. Return control: "Product spec drafted but has open dependencies. Needs [deliverable] from [Department] before finalizing."

## Step 5: Offer Next Steps

After generating:
- "Spec ready for review. Want me to start on Design specs based on this?"
- "Want me to break the acceptance criteria into engineering tasks?"
- "Any scope questions before we proceed to implementation?"

## Principles

**Specific beats comprehensive.** A 1-page spec with testable criteria is worth more than a 10-page PRD with vague requirements.

**Scope is the product.** What you exclude defines the feature as much as what you include. Always state Out of Scope explicitly.

**Metrics before launch.** If you can't measure success, you can't know if the feature worked. Define metrics and baselines before building.

**Edge cases are features.** Empty states, error states, and permission boundaries are not afterthoughts — they're part of the user experience.
