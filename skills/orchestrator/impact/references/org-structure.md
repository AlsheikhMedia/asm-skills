# Organization Structure

## 6-Core Default (Every Team)

These 6 functions exist in every software team, whether it's 1 person or 100. They map to the 6 core reference files.

| # | Function | What it covers | Reference |
|---|----------|---------------|-----------|
| 1 | **Product** | Specs, requirements, launch planning, pricing | `product.md` |
| 2 | **Engineering** | Code, schema, API, deployment, infrastructure | `engineering.md` |
| 3 | **Design** | UI, UX, prototypes, accessibility, design system | `design.md` |
| 4 | **QA** | Testing, regression, acceptance criteria | `qa.md` |
| 5 | **Marketing** | Content, campaigns, SEO, sales enablement | `marketing.md` |
| 6 | **Ops** | Analytics, security, legal, finance, support, research | `ops.md` |

For small teams: one person may own multiple functions. The analysis still surfaces the different *types of work* required — a founder handling Product + Marketing still needs to write the spec AND draft the announcement email.

## How to Override

The skill checks for org structure in this order:
1. `.claude/org-structure.md` in the project → Extended mode (custom departments)
2. Org references in the project's `CLAUDE.md`
3. This default (6-core)

To define a custom org, create `.claude/org-structure.md` with department names, what each owns, and known constraints.

---

## Extended: 14-Department Model

Loaded when `.claude/org-structure.md` exists or user says "extended" / "full org". A comprehensive 8-workstream + engineering functions model for growing teams.

### Foundation Layer

Must be settled before execution-layer work begins. Only triggered when the initiative changes something fundamental.

**1. Research** — ICP profiles, competitor matrix, pain point mapping, market sizing
**2. Brand** — Positioning, messaging framework, tone of voice, visual identity (standalone — serves all workstreams)
**3. Legal** — ToS, privacy policy, compliance, contracts, data handling
**4. Finance** — Unit economics, pricing model, cost structure, revenue projections

### Execution Layer

Runs after foundation decisions. Can run in parallel with each other.

**5. Content/Marketing** — SEO, blog, social, email sequences, campaigns, landing pages
**6. Sales** — Outreach, demos, pipeline management, sales enablement
**7. Product** — Launch checklists, pricing page, feature comparison, roadmap, specs
**8. Customer Success** — Onboarding, training, support docs, knowledge base, retention

### Engineering Functions (Cross-Cutting)

**9. Development** — Build scope, implementation, code quality, effort estimation
**10. QA/Testing** — Test scenarios, regression, coverage, acceptance criteria
**11. Design/UX** — UI changes, prototypes, design system, accessibility
**12. DevOps/Infrastructure** — Hosting, CI/CD, monitoring, deployment, feature flags
**13. Analytics** — Tracking events, KPI dashboards, data pipelines, experiment measurement
**14. Security** — Data handling, auth changes, vulnerability assessment, compliance

### Phase-Gating Rules

- Foundation Layer only triggered when: new market, new pricing, new data handling, new compliance requirement
- Most feature-level work starts at Execution + Engineering layers

### Typical Feature Profiles (Extended)

| Feature Type | Typical Departments | Foundation? |
|-------------|-------------------|-------------|
| UI/UX improvement | Design, Dev, QA, Product | No |
| New feature | Product, Dev, Design, QA, DevOps, Content, CS | Rarely |
| New product/vertical | All 14 | Yes |
| Infrastructure sprint | Dev, DevOps, QA, Product | No |
| Marketing campaign | Content, Design, Sales, Analytics | Maybe Brand |
| Pricing change | Finance, Product, Dev, Content, Sales, Legal | Yes |
| Data/compliance change | Legal, Security, Dev, DevOps, Product | Yes |
