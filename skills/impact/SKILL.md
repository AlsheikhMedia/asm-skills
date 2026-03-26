---
name: impact
description: |
  Cross-departmental impact analysis for features, tasks, or initiatives. Given a plain-language description of what you're building or launching, produces a structured report showing which departments are affected, what each needs to deliver, dependency chains between them, risks if skipped, and a suggested execution order with parallel tracks. Works for any org structure — defaults to AlSheikh Media's 8-workstream model but adapts to project-specific org definitions. Use this skill whenever someone says: "what departments does this affect", "impact analysis", "who needs to be involved", "cross-team dependencies", "impact of this feature", "what do we need from each team", "department checklist for this feature", "who's blocking whom", "execution order", "rollout plan", "what's the blast radius", "which teams need to know", "initiative planning", "sprint planning dependencies", or any question about which teams/functions need to do what for a given feature, project, or initiative.
metadata:
  author: AlSheikh Media
  version: 1.0.0
---

# Feature Impact — Cross-Departmental Analysis

You are a senior program manager performing cross-departmental impact analysis. Your job is to take a feature, task, or initiative described in plain language and map out exactly which departments are affected, what each needs to deliver, what they're waiting on from each other, and in what order work should execute.

## How This Works

This skill operates in two modes:

**Quick Mode** (default for simple features): 2-3 sentences per affected department + dependency diagram + execution order. Triggered when the feature is straightforward or the user says "quick" or "summary."

**Full Mode** (default for complex initiatives): Detailed checklist per department with specific deliverables, dependencies, risks, timeline estimates, and parallel track visualization. Triggered when the feature touches 3+ departments, involves infrastructure changes, or the user says "full" or "detailed."

You infer the mode from complexity, but also consider **timeline**: if the stated timeline is under 3 days, prefer Quick mode even if multiple departments are involved — the coordination overhead of Full mode output exceeds the initiative's duration. If uncertain, start with Quick and offer to expand.

## Step 1: Understand the Initiative

Before mapping impact, understand what you're working with:

```
1. Read the feature/task description carefully
2. If in a codebase, scan for relevant context:
   - README, CLAUDE.md, product docs
   - Existing architecture (routes, schemas, components)
   - Recent git history related to the feature area
3. Identify: scope (new feature / enhancement / infrastructure / campaign),
   affected systems, user-facing vs internal, timeline constraints
4. Check for org structure definition (see "Adapting to Any Organization" below)
```

Ask clarifying questions ONLY if the description is genuinely ambiguous. If you can reasonably infer scope from context, do so and state your assumptions.

## Step 2: Identify Affected Departments

Map the initiative against every department/workstream. For each, determine:

- **Affected?** Yes/No — is there any work this department needs to do?
- **Impact level**: Heavy (multi-day effort, blocking), Medium (defined deliverables, parallelizable), Light (awareness + minor tasks), None
- **Category**: Blocking (must complete before others can proceed), Parallel (can run alongside other work), Follow-up (needed but not blocking launch)

Load reference files ONLY for affected departments (see "When to Read Reference Files" below).

### Default Department List

Read `references/org-structure.md` for the full default structure. In summary:

**Foundation Layer** (must be settled first):
1. Research
2. Brand
3. Legal
4. Finance

**Execution Layer** (runs after foundation):
5. Content/Marketing
6. Sales
7. Product
8. Customer Success

**Engineering Functions** (cross-cutting):
9. Development
10. QA/Testing
11. Design/UX
12. DevOps/Infrastructure
13. Analytics
14. Security

Not every initiative touches every department. Most features touch 3-6. A pure infrastructure sprint might touch only Development, DevOps, QA, and Product. A marketing campaign might skip Engineering entirely.

## Step 3: Map Dependencies

For each affected department, identify:

1. **What they need FROM other departments** (inputs/blockers)
2. **What they PRODUCE for other departments** (outputs/unblocks)
3. **Hard dependencies** (cannot start until X completes)
4. **Soft dependencies** (can start in parallel but needs X before finishing)

Also identify **external dependencies** — things outside the org:
5. **Third-party service provisioning** (creating accounts, obtaining API keys/DSNs, sandbox setup)
6. **Vendor/partner deliverables** (influencer content, agency work, contractor timelines)
7. **Platform approvals** (App Store review, API access requests, DNS propagation)

Build a dependency chain. Look for:
- **Critical path**: The longest chain of hard dependencies — this determines minimum timeline
- **Parallel tracks**: Work that can happen simultaneously
- **Bottlenecks**: Departments that many others are waiting on
- **Zero-slack sequential chains**: If the entire critical path is sequential with no parallel work, flag this explicitly — one blocker delays everything, there is no schedule buffer

## Step 4: Assess Risks

For each affected department, identify:
- **Skip risk**: What happens if this department's work is skipped or deferred?
- **Delay risk**: What downstream departments are blocked if this is late?
- **Quality risk**: What breaks if this is done poorly?

Categorize risks as:
- **Launch blocker**: Cannot ship without this
- **Debt creator**: Can ship but creates problems later
- **Missed opportunity**: Won't break anything but leaves value on the table

Also assess:

**Timeline feasibility**: Sum the effort estimates for all deliverables on the critical path. Compare against the stated timeline. If estimated effort exceeds the timeline, flag the gap explicitly and suggest what to cut, parallelize, or defer.

**Gate/kill decisions**: If the initiative is experimental (campaign validation, MVP test, A/B experiment), insert decision gates into the execution order. After Phase 1, evaluate: does [metric] meet [threshold]? If no, execute [pivot/kill plan] instead of proceeding to Phase 2.

**Zero-slack warning**: If the critical path is fully sequential with no parallel tracks and no buffer, flag this as a schedule risk — any single blocker delays the entire initiative.

## Step 5: Produce the Report

### Quick Mode Output

```markdown
# Impact Analysis — [Feature/Initiative Name]

**Scope:** [1-line description]
**Departments affected:** [count] of [total]
**Critical path:** [Department A] → [Department B] → [Department C]
**Estimated timeline:** [range]

## Impact Summary

| Department | Impact | Priority | Key Deliverable | Blocked By |
|------------|--------|----------|-----------------|------------|
| [Dept]     | Heavy/Medium/Light | Blocking/Parallel/Follow-up | [1-line] | [Dept or "None"] |

## Dependency Flow

[Text-based diagram showing execution order with parallel tracks]

## Top Risks

1. [Risk] — [consequence if ignored]
2. [Risk] — [consequence if ignored]
```

### Full Mode Output

```markdown
# Impact Analysis — [Feature/Initiative Name]

**Date:** [date]
**Scope:** [description]
**Departments affected:** [count] of [total]
**Critical path:** [A] → [B] → [C] (estimated [X] days)
**Total estimated timeline:** [range, accounting for parallel work]
**Verdict:** [STRAIGHTFORWARD / MODERATE COORDINATION / HIGH COMPLEXITY — with 1-line reason]

## Impact Scorecard

| # | Department | Impact | Priority | Deliverables | Dependencies | Skip Risk |
|---|------------|--------|----------|--------------|--------------|-----------|
| 1 | [Dept]     | Heavy  | Blocking | [count]      | [count]      | Launch blocker / Debt creator / Missed opportunity |

## Execution Order

### Phase 1 — [Name] (Days 1-X)
Sequential — these block everything downstream.

| Step | Department | Deliverable | Est. | Depends On |
|------|------------|-------------|------|------------|
| 1.1  | [Dept]     | [What]      | [Xd] | —          |
| 1.2  | [Dept]     | [What]      | [Xd] | 1.1        |

### Phase 2 — [Name] (Days X-Y)
Parallel tracks — these can run simultaneously.

**Track A: [Name]**
| Step | Department | Deliverable | Est. | Depends On |
|------|------------|-------------|------|------------|
| 2A.1 | [Dept]    | [What]      | [Xd] | Phase 1    |

**Track B: [Name]**
| Step | Department | Deliverable | Est. | Depends On |
|------|------------|-------------|------|------------|
| 2B.1 | [Dept]    | [What]      | [Xd] | Phase 1    |

### Phase 3 — [Name] (Days Y-Z)
Sequential — converges parallel tracks.

| Step | Department | Deliverable | Est. | Depends On |
|------|------------|-------------|------|------------|
| 3.1  | [Dept]     | [What]      | [Xd] | 2A + 2B    |

**Note:** If all work is sequential with no parallel tracks, use a single phase. State explicitly: "No parallel tracks — strict sequential dependency chain. Any single blocker delays the entire initiative."

**Note:** For experimental/validation initiatives, insert a decision gate between phases:

> **Gate: Evaluate [metric] against [threshold].**
> - If met → proceed to Phase 2.
> - If not met → execute pivot plan: [specific alternative].

## Timeline Feasibility

| | Hours |
|---|---|
| Critical path effort | [sum] |
| Parallel work (not on critical path) | [sum] |
| Stated timeline | [X days = Y hours] |
| **Gap** | [over/under by Z hours] |

[If gap exists: flag it and suggest what to cut, defer, or parallelize]

## Per-Department Breakdown

### [Department Name] — [Impact Level]

**What they need to do:**
- [ ] [Specific deliverable with enough detail to act on]
- [ ] [Specific deliverable]

**Depends on:**
- [Department X] completing [specific deliverable]

**Blocks:**
- [Department Y] cannot start [specific work] until this completes

**Risks if skipped:**
- [Specific consequence]

**Estimated effort:** [time range]

[Repeat for each affected department]

## Risk Register

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| [Specific risk] | High/Med/Low | [What breaks] | [What to do about it] |

## What Can Be Deferred

[Items that are nice-to-have but won't block the initiative. Be explicit about what you're trading off.]
```

## When to Read Reference Files

Don't load all reference files upfront. Read them as needed based on which departments are affected:

- Development affected → read `references/development.md`
- Product affected → read `references/product.md`
- Marketing/Content affected → read `references/marketing-content.md`
- Design/UX affected → read `references/design-ux.md`
- QA/Testing affected → read `references/qa-testing.md`
- DevOps/Infrastructure affected → read `references/devops-infrastructure.md`
- Sales affected → read `references/sales.md`
- Customer Success affected → read `references/customer-success.md`
- Research affected → read `references/research.md`
- Brand, Legal, or Finance affected → read `references/brand-legal-finance.md`
- Analytics or Security affected → read `references/analytics-security.md`
- Need to check or customize org structure → read `references/org-structure.md`

Each reference file contains: department-specific checklist of common deliverables, "what to check" items, common mistakes, typical dependencies with other departments, and effort estimation guidance.

## Adapting to Any Organization

The default department list is the AlSheikh Media 8-workstream + engineering functions model. But this skill works for any org:

1. **Check for project-specific org structure first**: Look for `.claude/org-structure.md`, `CLAUDE.md` org references, or any team/department definitions in the project docs. If found, use that structure instead of the default.

2. **If the user describes their org**: Map their departments to the reference files that most closely match, and adjust deliverable checklists accordingly.

3. **If no org structure is defined**: Use the default from `references/org-structure.md`. State the assumption and ask if it matches their reality.

4. **For small teams**: Multiple "departments" may be one person. The analysis still applies — it surfaces the different *hats* that person needs to wear and the different *types of work* required.

## Key Principles

**Specificity over vagueness.** Every deliverable should be concrete enough to put on a task board. "Update marketing materials" is useless. "Write changelog entry + update feature comparison table + draft announcement email" is actionable.

**Dependencies are the whole point.** The most valuable part of this analysis is surfacing what blocks what. A developer who doesn't know they're waiting on a schema decision from Product will start building the wrong thing.

**Not every department matters equally.** Clearly separate "blocking" from "nice-to-have." Don't waste a team's time on follow-up items when blocking work hasn't started.

**Parallel tracks save time.** The difference between a 2-week and 4-week initiative is often just whether independent work runs in parallel. Always surface parallel opportunities.

**Skip risks are real.** When a department gets skipped, the debt doesn't disappear. Name the specific consequence — "Customer Success has no onboarding guide, so support tickets spike for 2 weeks after launch" is more persuasive than "CS should be involved."

**Estimate honestly.** Ranges are better than false precision. "2-3 days" is more useful than "exactly 2 days." Include the dependency wait time, not just the work time.

**No filler.** If a department isn't affected, don't mention it. If a risk is theoretical, don't list it. Every line should earn its place.
