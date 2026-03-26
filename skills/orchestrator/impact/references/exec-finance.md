# Finance — Execution Module

Load this when the impact execution loop needs to analyze pricing, unit economics, revenue projections, and cost structure.

> **Disclaimer:** These are estimates and frameworks, not financial advice. Consult an accountant for tax and compliance matters.

## Workflow

### Step 1: Detect Mode

Classify the request:

1. **Pricing Design** — set or restructure pricing
2. **Unit Economics** — LTV, CAC, margins, payback period
3. **Revenue Projection** — MRR/ARR forecast model
4. **Cost Analysis** — understand the cost structure
5. **Break-Even** — when profitability is reached

If the request spans multiple modes (common — "how should I price this" often needs pricing + unit economics + break-even), run them in sequence and cross-reference.

### Step 2: Gather Context

Before running numbers:

1. **Scan the project** for product context: README, feature lists, pricing pages, Stripe integration, plan definitions in code
2. **Check for existing financial context**: any pricing configs, plan tiers in the codebase, billing-related schemas
3. **Identify the business model**: SaaS / marketplace / e-commerce / service / API — this determines which metrics matter
4. **Look for competitor signals**: if there's a competitive analysis doc, `.claude/product-marketing-context.md`, or similar

Ask for missing critical inputs — but only what you genuinely need:
- For **pricing**: target customer, value delivered, cost to serve, competitive landscape
- For **unit economics**: current customer count, ARPU, acquisition channels, churn rate
- For **revenue projection**: current MRR, growth rate, churn, planned pricing changes
- For **cost analysis**: hosting costs, tool subscriptions, salaries (if any), per-customer variable costs

### Step 3: Analyze

#### Pricing Design Mode

Use the Pricing Models Comparison and Psychology sections below. Then:

1. **Match model to business**: freemium / per-seat / usage-based / flat-rate / tiered — based on value delivery pattern
2. **Design tiers** (if tiered): 3 max. Each needs a clear persona and upgrade trigger.
3. **Set prices**: anchor to value, not cost
4. **Validate with unit economics**: run unit economics for each tier
5. **Output**: tier comparison table with personas, prices, features, margins, and highlighted recommended tier

#### Unit Economics Mode

Calculate and show in a table:

ARPU -> CAC -> Cost to serve -> Gross margin -> LTV (ARPU x margin / churn) -> LTV:CAC (target > 3:1) -> Payback period (CAC / monthly gross profit)

Every metric gets a value column AND a formula column. End with a verdict: Healthy / Needs improvement / Unsustainable — with specific fix if unhealthy.

#### Revenue Projection Mode

Build a 12-month MRR model. State assumptions (starting MRR, new customers/mo, churn, ARPU), then output month-by-month table: customers, new, churned, MRR, cumulative revenue. End with Month 12 MRR, ARR, and total Year 1 revenue.

#### Cost Analysis Mode

Itemize every cost:

1. **Fixed costs**: hosting, domains, tools, subscriptions (monthly)
2. **Variable costs**: per-customer — support, API calls, storage, transaction fees
3. **One-time costs**: setup, migration, legal, branding
4. **Monthly burn rate**: fixed + (variable x customers)

#### Break-Even Mode

Output: fixed costs, price per unit, variable cost, contribution margin, break-even customer count, and estimated months to reach it at current growth rate.

### Step 4: After Analysis

Ask:

1. **Scenario modeling?** "Want me to model what happens if you raise prices 20%? Or if churn drops by 2%?"
2. **Pricing page?** "Want me to generate the pricing page copy and component?"
3. **Save it?** "Want me to save this analysis to a file for reference?"

## Templates

### Pricing Models Comparison

| Model | How it works | Best for | Pros | Cons |
|-------|-------------|----------|------|------|
| **Freemium** | Free tier + paid upgrade | Products with viral/network effects, low marginal cost | Large top-of-funnel, self-serve growth | Low conversion (2-5%), support cost on free users |
| **Per-Seat** | Price x number of users | Collaboration tools, team-based products | Revenue scales with adoption, predictable | Discourages inviting teammates, gaming with shared accounts |
| **Usage-Based** | Pay for what you use (API calls, storage, events) | Infrastructure, APIs, variable-consumption products | Fair, scales naturally, low barrier to start | Unpredictable revenue, customer bill anxiety |
| **Flat-Rate** | One price, everything included | Simple products, single-persona tools | Easy to understand, no decision fatigue | Leaves money on table from power users, hard to upsell |
| **Tiered** | 2-4 plans with feature/limit gates | Most SaaS — different personas with different needs | Captures different willingness-to-pay, clear upgrade path | Complexity, "which plan?" friction, feature allocation decisions |

#### When to Use Each

- **You have a product with near-zero marginal cost** -> Freemium (if viral) or Flat-Rate (if not)
- **Value scales linearly with team size** -> Per-Seat
- **Value scales with consumption** -> Usage-Based (or hybrid: base + usage)
- **You serve 2-3 distinct personas** -> Tiered
- **You're unsure** -> Start with Flat-Rate, add tiers later when you understand your customers

### SaaS Metrics — Formulas

| Metric | Formula | What it tells you |
|--------|---------|-------------------|
| **MRR** | Sum of all monthly recurring revenue | Current monthly revenue run rate |
| **ARR** | MRR x 12 | Annualized revenue (use for context, not projection) |
| **ARPU** | Total MRR / total paying customers | Average revenue per customer per month |
| **Churn Rate** | Customers lost in period / customers at start of period | % of customers leaving per month |
| **Revenue Churn** | MRR lost in period / MRR at start of period | % of revenue leaving per month (can differ from customer churn) |
| **LTV** | ARPU x Gross Margin / Monthly Churn Rate | Total revenue expected from one customer over their lifetime |
| **CAC** | Total acquisition spend / new customers acquired | Cost to acquire one customer |
| **LTV:CAC** | LTV / CAC | Return on acquisition investment (target: > 3:1) |
| **Payback Period** | CAC / (ARPU x Gross Margin) | Months to recoup acquisition cost |
| **NRR** | (Starting MRR + expansion - contraction - churn) / Starting MRR x 100 | Net revenue retention — above 100% means growth without new customers |
| **Gross Margin** | (Revenue - COGS) / Revenue | Percentage of revenue that's actual profit after direct costs |

### Unit Economics Template

```
Revenue per customer:     ${ARPU}/mo
Cost to acquire:          ${CAC}
Cost to serve:            ${serving_cost}/mo
  - Hosting:              ${hosting} / {customers} = ${per_customer}
  - Support:              ${support_hours} x ${hourly_rate} / {customers}
  - Third-party APIs:     ${api_cost_per_customer}
  - Transaction fees:     ${ARPU} x {stripe_rate} = ${fees}
Gross margin:             (${ARPU} - ${serving_cost}) / ${ARPU} = {X}%
LTV:                      ${ARPU} x {margin} / {churn} = ${LTV}
LTV:CAC:                  ${LTV} / ${CAC} = {ratio}:1
Payback:                  ${CAC} / (${ARPU} x {margin}) = {months} months
```

### Pricing Psychology

#### Anchor Pricing
Present the most expensive tier first (or a "Contact Us" enterprise tier). This makes the middle tier feel reasonable by comparison. The middle tier should be the one you want most people to choose.

#### Decoy Effect
If you have two tiers and people cluster on the cheaper one, add a third tier between them that's slightly worse value than the target tier. This pushes people toward the one you want them to pick.

#### Price Endings
- **$X9/mo** ($19, $49, $99): signals value/deal — good for SMB, consumer, price-sensitive markets
- **$X0/mo** ($20, $50, $100): signals quality/premium — good for B2B, professional tools
- **$X7/mo** ($17, $47, $97): signals indie/bootstrapped — good for creator/solopreneur tools

#### Tier Naming
| Name style | Signal | Example |
|------------|--------|---------|
| Descriptive | Clarity, professional | Free, Starter, Professional, Enterprise |
| Size-based | Growth path | Solo, Team, Business |
| Metaphorical | Brand personality | Seed, Grow, Scale |

Avoid clever-but-confusing names. "What's the difference between Voyager and Explorer?" is a question you don't want.

#### Annual vs Monthly
- Annual discount of 15-20% is standard
- Frame as "2 months free" rather than "17% off" — concrete > abstract
- Annual billing reduces churn mechanically (harder to cancel mid-year)
- Improves cash flow: $228 today vs $19/mo over 12 months

### Break-Even Formula

```
Break-even (units) = Fixed Costs / (Price - Variable Cost per Unit)
Break-even (revenue) = Fixed Costs / Gross Margin %
Break-even (months) = Fixed Costs / (MRR - Variable Costs)
```

#### Break-Even Example
- Fixed costs: $500/mo (hosting, tools, subscriptions)
- Price: $29/mo per customer
- Variable cost: $3/mo per customer (Stripe fees, API costs, storage)
- Contribution margin: $29 - $3 = $26/customer
- Break-even: $500 / $26 = **20 customers**

At 4 new customers/month with 5% churn: break-even at month 6.

## Principles

**Price on value, not cost.** What is it worth to the customer? A tool that saves a business $10,000/year can charge $1,000/year regardless of whether it costs $5/month to host. Cost sets your floor; value sets your ceiling.

**Show the math.** Every number should have a visible formula. "LTV is $450" means nothing without "ARPU ($50) x Gross Margin (90%) / Churn (10%) = $450." The founder needs to plug in their own numbers next quarter.

**Conservative projections.** Use pessimistic growth, realistic churn, and no hockey sticks. If the model works with conservative assumptions, the founder can be pleasantly surprised. If it only works with optimistic assumptions, it doesn't work.

**Unit economics before scale.** If LTV < CAC at 10 customers, it won't fix itself at 1,000. Fix the fundamentals first: increase ARPU, reduce cost to serve, reduce churn, or find cheaper acquisition channels.

**Three tiers is a strategy, not a default.** Only recommend tiered pricing if each tier targets a different persona with different willingness to pay. Two tiers with a clear free/paid boundary often outperforms three tiers with blurry distinctions.

## Example

**Task**: "How should I price my SaaS?"
Context scan reveals: project management tool for freelancers, Stripe integration, three plan definitions in code (Free, Pro $12/mo, Team $29/mo), 47 paying customers, ~8% monthly churn.

```markdown
## Pricing Analysis — TaskFlow

> Disclaimer: Estimates and frameworks, not financial advice. Consult an accountant for tax/compliance.

### Current State
- 47 paying customers, blended ARPU: $18.50/mo, MRR: $869.50
- Monthly churn: 8% (high — target is 3-5%)

### Pricing Recommendation

**Model:** Tiered — fits the freelancer -> small team growth path

| | Free | Pro | Business |
|---|------|-----|----------|
| **For** | Solo freelancer exploring | Active freelancer, daily use | Small team (2-5) |
| **Price** | $0 | $19/mo (up from $12) | $39/mo (up from $29) |
| **Upgrade trigger** | Hits 3 project limit | Adds first team member | Needs reporting or 3+ seats |

**Why raise prices:** Pro at $12 is underpriced for a daily-use professional tool. The $7 increase on 47 customers = $329/mo additional MRR immediately.

### Unit Economics (Pro at $19/mo)

| Metric | Value | Formula |
|--------|-------|---------|
| CAC | $45 (est.) | Content marketing + trial conversion |
| Gross margin | 91% | ($19 - $1.70) / $19 |
| LTV | $216 | $19 x 0.91 / 0.08 |
| LTV:CAC | 4.8:1 | Healthy — above 3:1 threshold |
| Payback | 2.6 months | $45 / ($19 x 0.91) |

**Break-even:** $380/mo fixed costs / $17.29 margin = 22 customers. Currently at 47 -> **profitable at ~$433/mo net.**

### Top Recommendations
1. Raise Pro to $19, Business to $39 — grandfather existing for 3 months
2. Fix churn: 8% -> 5% is worth more than doubling acquisition (LTV jumps to $346)
3. Add annual billing at 20% discount: improves cash flow, reduces churn mechanically
```
