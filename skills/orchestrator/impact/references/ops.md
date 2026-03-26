# Ops — Impact Checklist

Covers cross-cutting operational functions. Load this when Analytics, Security, Legal, Finance, Brand, Research, or Customer Success are affected.

## When to Skip

Skip if: Pure feature development with no new data collection, no pricing change, no compliance implications, no customer-facing behavior change, and no new tracking events.

## Analytics

These two cross-cutting engineering functions — Analytics and Security — share a pattern: both are frequently forgotten until after launch, and both are cheaper to address during development than after.

**Typically affected when:** new user-facing feature, new pages, campaign launch
**Skip if:** no new user actions to track, no new pages, no campaign

### What to Check
- [ ] Tracking events defined (what user actions need to be measured?)
- [ ] Event naming convention followed (consistent with existing events)
- [ ] KPI dashboard update needed (new metrics to display)
- [ ] Success metrics instrumented before launch (not after)
- [ ] Funnel tracking updated (if user flow changes)
- [ ] A/B test measurement set up (if feature is being tested)
- [ ] Data pipeline impact assessed (new event volume, storage needs)
- [ ] Attribution tracking for campaigns (UTM parameters, conversion events)

### Analytics needs FROM:

| Department | What | Why |
|-----------|------|-----|
| Product | Success metrics definition, KPIs to track | Analytics needs to know what to measure |
| Development | Event implementation in code | Analytics can't track what isn't instrumented |
| Marketing/Content | Campaign tracking requirements, attribution needs | Analytics needs to measure campaigns |

### Analytics PRODUCES for:

| Department | What | Why |
|-----------|------|-----|
| Product | Feature usage data, adoption metrics, funnel analysis | Product needs data for decisions |
| Marketing/Content | Campaign performance data, conversion metrics | Marketing needs to optimize |
| Sales | Usage data, engagement metrics for customer conversations | Sales uses data as proof points |

### Common Deliverables
- [ ] Event tracking plan (event name, properties, trigger conditions)
- [ ] Dashboard update or creation
- [ ] Funnel definition update
- [ ] Data validation (events firing correctly)
- [ ] Baseline metrics captured (before vs. after comparison)

### Common Mistakes
- No tracking plan before launch (adding events after = incomplete data)
- Inconsistent event naming ("user_signup" vs. "userSignup" vs. "signup_complete")
- Tracking too much (noise) or too little (can't answer key questions)
- No baseline measurement (can't prove impact without before/after data)
- Dashboard not accessible to non-technical stakeholders

## Security

**Typically affected when:** auth changes, new data types, new API endpoints, third-party integrations
**Skip if:** no auth changes, no new data types, no new API endpoints, no third-party integrations

### What to Check
- [ ] Auth changes reviewed (new roles, permissions, access patterns)
- [ ] Data handling assessed (PII, sensitive data, encryption needs)
- [ ] Input validation implemented (injection, XSS, CSRF prevention)
- [ ] API rate limiting configured (abuse prevention)
- [ ] Third-party integration security reviewed (API key storage, data sharing)
- [ ] Session management impact (new auth flows, token handling)
- [ ] Secrets management (no hardcoded credentials, proper env var usage)
- [ ] Error messages don't leak sensitive information
- [ ] File upload validation (if applicable — type, size, content scanning)

### Security needs FROM:

| Department | What | Why |
|-----------|------|-----|
| Development | Code review access, architecture documentation | Security needs to understand what's being built |
| Legal | Compliance requirements, data classification | Security needs to know what rules apply |
| DevOps | Infrastructure access, monitoring capability | Security needs visibility into systems |

### Security PRODUCES for:

| Department | What | Why |
|-----------|------|-----|
| Development | Security requirements, vulnerability findings | Dev needs to fix before launch |
| DevOps | Security config requirements, monitoring rules | DevOps implements security at infra level |
| Legal | Security posture assessment, compliance evidence | Legal needs proof of compliance |
| Product | Scope constraints from security requirements | Product needs to know security boundaries |

### Common Deliverables
- [ ] Security review of new code (auth, data handling, input validation)
- [ ] Threat model for new feature (what could go wrong?)
- [ ] Secrets audit (no credentials in code or logs)
- [ ] Penetration test scope update (if new attack surface)
- [ ] Security documentation update (for compliance audits)

### Common Mistakes
- Auth changes without security review (permission escalation bugs)
- New data collection without encryption assessment
- Third-party API keys stored in code (instead of environment variables)
- No rate limiting on new endpoints (abuse vector)
- Error messages exposing stack traces or internal state in production
- File uploads without type/size validation (storage abuse, malicious files)
- Assuming the framework handles security (it handles some, not all)

### Effort Estimation (Analytics & Security)

| Deliverable | Typical Range |
|------------|--------------|
| Tracking event plan | 0.5-1 day |
| Event implementation | 0.5-1 day per feature area |
| Dashboard creation | 0.5-1 day |
| Security code review | 0.5-2 days |
| Threat model | 0.5-1 day |
| Penetration test | 2-5 days (often outsourced) |
| Secrets audit | 0.5 day |

## Brand

These three Foundation Layer workstreams — Brand, Legal, and Finance — share a trigger pattern: most feature-level work does NOT involve them. They're triggered only when an initiative changes something fundamental.

| Workstream | Trigger | Example |
|-----------|---------|---------|
| Brand | Messaging, positioning, or visual identity affected | New product line, rebrand, new market |
| Legal | Data handling, compliance, contractual obligations affected | New data collection, GDPR scope change, new billing terms |
| Finance | Pricing, cost structure, or revenue model affected | New tier, pricing change, new cost center |

**Typically affected when:** new product line, new data collection, pricing change, new market entry
**Skip if:** feature within existing product, no new data collection, no pricing change, no new market

### What to Check
- [ ] Messaging framework still accurate (positioning, value props, differentiators)
- [ ] Tone of voice consistent with new feature/initiative
- [ ] Visual identity applied correctly (colors, typography, logo usage)
- [ ] New product naming follows brand guidelines
- [ ] Co-branding or partner branding guidelines followed (if applicable)

### Brand PRODUCES for:
| Department | What | Why |
|-----------|------|-----|
| Marketing/Content | Messaging framework, tone guidelines, brand assets | Marketing must stay on-brand |
| Design/UX | Visual identity specs, color/typography tokens | Design must stay on-brand |
| Sales | Positioning statement, approved talking points | Sales must represent accurately |

### Common Mistakes
- Feature messaging inconsistent with brand positioning
- New product name not vetted against existing brand architecture
- Marketing creates off-brand content because brand guidelines weren't consulted

## Legal

### What to Check
- [ ] Terms of Service update needed (new feature changes what users agree to)
- [ ] Privacy Policy update needed (new data collected, new processing purpose)
- [ ] Data Processing Agreement (DPA) impact assessed (B2B enterprise feature)
- [ ] Compliance requirements identified (GDPR, CCPA, local regulations)
- [ ] Data retention policy applies to new data types
- [ ] Third-party data sharing implications (new integrations, analytics)
- [ ] Contractual obligations affected (SLA changes, feature guarantees)
- [ ] Cookie/tracking consent updated (new tracking pixels, analytics)

### Legal PRODUCES for:
| Department | What | Why |
|-----------|------|-----|
| Development | Data handling requirements, compliance constraints | Dev needs to know data rules before building schema |
| Product | Scope constraints, feature limitations from compliance | Product needs to scope within legal boundaries |
| Marketing/Content | Approved claims, testimonial rules, disclaimer text | Marketing can't publish unapproved claims |
| DevOps | Data storage/retention requirements | Infrastructure must comply |

### Common Mistakes
- Launching new data collection without privacy policy update
- Assuming existing ToS covers new feature (it often doesn't)
- Not reviewing third-party integration data sharing implications
- GDPR consent flow not updated for new data processing
- No legal review on marketing claims (especially around AI, performance, security)

## Finance

### What to Check
- [ ] Unit economics impact assessed (does this feature change margins?)
- [ ] Pricing model change needed (new tier, new feature gating)
- [ ] Cost structure impact (new services, higher compute, third-party fees)
- [ ] Revenue projection updated
- [ ] Budget allocation for initiative (engineering time, marketing spend, tools)
- [ ] Cash flow impact (if large upfront investment required)

### Finance PRODUCES for:
| Department | What | Why |
|-----------|------|-----|
| Product | Pricing decisions, tier placement, packaging rules | Product can't spec packaging without pricing |
| Sales | Approved pricing, discount guidelines, proposal templates | Sales needs accurate pricing |
| Marketing/Content | Pricing page content, comparison data | Marketing needs pricing to publish |

### Common Mistakes
- Pricing change without unit economics validation (margin erosion)
- No cost estimate for third-party services (surprise bills at scale)
- Feature added to all tiers when it should be premium (leaves money on the table)
- No budget for marketing/launch alongside feature development

## Research

When a feature, task, or initiative affects the Research workstream, use this checklist to identify specific deliverables, dependencies, and risks.

Research is a Foundation Layer workstream. Most feature-level work does NOT trigger Research — it's only involved when the initiative changes something fundamental about who you're serving, what market you're in, or what competitors you're facing.

**Typically affected when:** new product or product line, new market segment, competitive landscape shift, pricing model overhaul
**Skip if:** feature within existing product for existing market, no new data types, no competitive positioning shift

### When Research Is Triggered

- New product or product line
- New market segment or geography
- Significant pivot in target customer
- Competitive landscape shift (new entrant, acquisition, feature parity)
- Pricing model overhaul
- New vertical or industry expansion

### What to Check

#### ICP & Market
- [ ] ICP profiles need updating (new segment, changed personas)
- [ ] Pain point mapping needs refresh
- [ ] Market sizing needs revision
- [ ] Customer interview data needed (validation before build)

#### Competitive
- [ ] Competitor matrix needs updating
- [ ] New competitor entered the space
- [ ] Competitive gap analysis needed (what we have vs. don't)
- [ ] Competitor pricing research needed

#### Validation
- [ ] Feature concept validated with target users
- [ ] Willingness-to-pay tested (if pricing implications)
- [ ] Alternative solutions users currently use documented
- [ ] Switching costs understood

### Typical Dependencies

**Research PRODUCES for:**

| Department | What | Why |
|-----------|------|-----|
| Product | Validated ICP, pain points, competitive gaps | Product specs need to solve real problems |
| Brand | Market language, positioning data | Brand messaging needs market context |
| Marketing/Content | ICP language, pain points, competitor positioning | Content must resonate with target audience |
| Sales | Target account criteria, competitive intel | Sales needs to know who to call and what to say |
| Finance | Market sizing, pricing research | Financial models need market data |

**Research needs FROM:**

| Department | What | Why |
|-----------|------|-----|
| Sales | Field feedback, prospect objections, lost deal reasons | Research needs real-world signal |
| Customer Success | Customer feedback, usage patterns, churn reasons | Research needs retention signal |
| Product | Feature usage data, adoption metrics | Research needs product signal |

### Effort Estimation Guide

| Research Type | Typical Range |
|--------------|--------------|
| Competitive analysis refresh | 1-2 days |
| Customer interview round (5 interviews) | 1-2 weeks |
| Market sizing | 1-3 days |
| Pricing research | 2-5 days |

### Common Mistakes

- Building without validating (assumption-driven development)
- Using outdated competitor data (market moves fast)
- ICP is too broad ("SMBs" vs. "B2B companies with 50-200 employees in your target market")
- No re-validation after pivot (research from 6 months ago may not apply)
- Research done but not shared (stays in a doc nobody reads)

## Customer Success

When a feature, task, or initiative affects Customer Success, use this checklist to identify specific deliverables, dependencies, and risks.

**Typically affected when:** user-facing behavior change, new feature customers will interact with, breaking change
**Skip if:** internal tooling, infrastructure change, backend-only, no change to user experience

### What to Check

#### Support Readiness
- [ ] Knowledge base article created or updated
- [ ] Internal FAQ prepared (answers to likely customer questions)
- [ ] Support ticket categories updated (if new feature area)
- [ ] Escalation paths defined (who handles issues with this feature)
- [ ] Known limitations documented (what doesn't work yet)
- [ ] Workaround guidance prepared (for known issues)

#### Onboarding Updates
- [ ] Onboarding flow changes needed (new steps, removed steps)
- [ ] In-app guidance updated (tooltips, walkthroughs, empty states)
- [ ] Training materials updated (video guides, written guides)
- [ ] Demo environment reflects new feature
- [ ] First-use experience designed (what happens when they try it for the first time)

#### Customer Communication
- [ ] Proactive outreach planned (notify affected customers before change)
- [ ] Migration guide written (if workflow changes significantly)
- [ ] Change notification drafted (in-app banner, email, or both)
- [ ] Feedback collection mechanism set up (survey, in-app prompt)

#### Health & Retention
- [ ] Health score impact assessed (does this feature affect key health indicators?)
- [ ] Churn risk identified (if removing/changing existing behavior)
- [ ] Adoption tracking defined (how do we know customers are using it?)
- [ ] Success criteria for customers (what does "successfully using this" look like?)

### Typical Dependencies

**Customer Success needs FROM:**

| Department | What | Why |
|-----------|------|-----|
| Product | Feature docs, known limitations, rollout timeline | CS needs to know what to tell customers |
| Development | Feature behavior details, known edge cases | CS needs to troubleshoot accurately |
| Marketing/Content | Announcement content, positioning | CS shares announcements with customers |
| Design/UX | Updated UX flows, in-app guidance specs | CS needs to walk customers through new UX |

**Customer Success PRODUCES for:**

| Department | What | Why |
|-----------|------|-----|
| Product | Customer feedback, usage patterns, pain points | Product needs field intelligence |
| Development | Bug reports from customers, edge cases found in production | Dev needs real-world bug reports |
| Sales | Success stories, reference customers, adoption metrics | Sales uses proof points to close deals |

### Common Deliverables by Initiative Type

#### New Feature
- [ ] Knowledge base article
- [ ] Internal FAQ
- [ ] Updated onboarding guide (if applicable)
- [ ] Customer announcement coordination with Marketing

#### Breaking Change
- [ ] Migration guide
- [ ] Proactive customer outreach list
- [ ] Support team training session
- [ ] Escalation procedure for migration issues

#### Infrastructure / Performance
- [ ] Usually no CS deliverables
- [ ] Exception: If downtime involved — customer notification + status page update

### Common Mistakes

- CS learns about feature at launch (should be briefed during development)
- No knowledge base article (customers search help docs first)
- Onboarding flow not updated (new users see outdated steps)
- No migration guide for breaking changes (support tickets spike)
- No feedback mechanism (can't improve what you don't measure)
- Assuming customers will read announcements (most won't — in-app nudge needed)
