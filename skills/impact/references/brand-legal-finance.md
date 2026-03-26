# Brand, Legal & Finance — Impact Checklist

These three Foundation Layer workstreams are grouped because they share a trigger pattern: most feature-level work does NOT involve them. They're triggered only when an initiative changes something fundamental.

## When Foundation Layer Is Triggered

| Workstream | Trigger | Example |
|-----------|---------|---------|
| Brand | Messaging, positioning, or visual identity affected | New product line, rebrand, new market |
| Legal | Data handling, compliance, contractual obligations affected | New data collection, GDPR scope change, new billing terms |
| Finance | Pricing, cost structure, or revenue model affected | New tier, pricing change, new cost center |

---

## Brand

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

---

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

---

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
