# Organization Structure — Default

This is the default AlSheikh Media organizational model used for impact analysis. If the project defines its own org structure, use that instead.

## How to Override

The skill checks for org structure in this order:
1. `.claude/org-structure.md` in the project
2. Org references in the project's `CLAUDE.md`
3. This default file

To define a custom org structure, create `.claude/org-structure.md` with department/team names, what each team owns, key contacts (optional), and known constraints (team size, availability).

## Default: AlSheikh Media 8-Workstream Model

### Foundation Layer

These must be settled before execution-layer work begins. "Settled" means decisions are made and documented — not that work is complete forever.

**1. Research**
- Owns: ICP profiles, competitor matrix, pain point mapping, market sizing
- Settles: Who we're building for, what they need, who else serves them

**2. Brand**
- Owns: Positioning, messaging framework, tone of voice, visual identity
- Settles: How we talk about ourselves, what we look/sound like
- Note: Brand is standalone (not under Marketing) — it serves ALL workstreams

**3. Legal**
- Owns: Terms of service, privacy policy, compliance, contracts, data handling
- Settles: What we can/can't do, what we must disclose, contractual obligations

**4. Finance**
- Owns: Unit economics, pricing model, cost structure, revenue projections
- Settles: What we charge, what things cost, whether the math works

### Execution Layer

Runs after foundation decisions are made. Can run in parallel with each other.

**5. Content/Marketing**
- Owns: SEO, blog, social media, email sequences, campaign creative, landing pages

**6. Sales**
- Owns: Outreach, demos, pipeline management, sales enablement materials

**7. Product**
- Owns: Launch checklists, pricing page, feature comparison, roadmap, specs, prioritization

**8. Customer Success**
- Owns: Onboarding flows, training materials, support docs, knowledge base, retention

### Engineering Functions (Cross-Cutting)

These serve all layers and can be involved at any phase.

**9. Development**
- Owns: Build scope, implementation, code quality, technical constraints, effort estimation

**10. QA/Testing**
- Owns: Test scenarios, regression testing, coverage, acceptance criteria verification

**11. Design/UX**
- Owns: UI changes, prototypes, design system updates, UX research, accessibility

**12. DevOps/Infrastructure**
- Owns: Hosting, CI/CD, monitoring, deployment, environment management, feature flags

**13. Analytics**
- Owns: Tracking events, KPI dashboards, data pipelines, experiment measurement

**14. Security**
- Owns: Data handling, auth changes, vulnerability assessment, compliance verification

## Phase-Gating Rules

- Foundation Layer decisions don't need to be revisited for every feature — only when the feature changes something fundamental (new market, new pricing, new data handling)
- Most feature-level work starts at the Execution + Engineering layers
- If a feature introduces a new product category, new compliance requirement, or new pricing model, it pulls in Foundation Layer departments

## Typical Feature Profiles

| Feature Type | Typical Departments | Foundation Involved? |
|-------------|-------------------|---------------------|
| UI/UX improvement | Design, Dev, QA, Product | No |
| New feature (existing product) | Product, Dev, Design, QA, DevOps, Content, CS | Rarely |
| New product/vertical | All 14 | Yes — full foundation review |
| Infrastructure sprint | Dev, DevOps, QA, Product | No |
| Marketing campaign | Content, Design, Sales, Analytics | Maybe Brand |
| Pricing change | Finance, Product, Dev, Content, Sales, Legal | Yes — Finance + Legal |
| Data/compliance change | Legal, Security, Dev, DevOps, Product | Yes — Legal |

## Small Team Adaptation

For teams where one person wears multiple hats, the analysis still applies. It surfaces the different *types of work* required. A founder handling Product + Sales + Marketing still needs to:
- Write the spec (Product hat)
- Update the demo script (Sales hat)
- Draft the announcement email (Marketing hat)

The value is in making each type of work explicit so nothing gets forgotten.
