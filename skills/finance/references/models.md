# Finance Models Reference

## Pricing Models Comparison

| Model | How it works | Best for | Pros | Cons |
|-------|-------------|----------|------|------|
| **Freemium** | Free tier + paid upgrade | Products with viral/network effects, low marginal cost | Large top-of-funnel, self-serve growth | Low conversion (2-5%), support cost on free users |
| **Per-Seat** | Price × number of users | Collaboration tools, team-based products | Revenue scales with adoption, predictable | Discourages inviting teammates, gaming with shared accounts |
| **Usage-Based** | Pay for what you use (API calls, storage, events) | Infrastructure, APIs, variable-consumption products | Fair, scales naturally, low barrier to start | Unpredictable revenue, customer bill anxiety |
| **Flat-Rate** | One price, everything included | Simple products, single-persona tools | Easy to understand, no decision fatigue | Leaves money on table from power users, hard to upsell |
| **Tiered** | 2-4 plans with feature/limit gates | Most SaaS — different personas with different needs | Captures different willingness-to-pay, clear upgrade path | Complexity, "which plan?" friction, feature allocation decisions |

### When to Use Each

- **You have a product with near-zero marginal cost** → Freemium (if viral) or Flat-Rate (if not)
- **Value scales linearly with team size** → Per-Seat
- **Value scales with consumption** → Usage-Based (or hybrid: base + usage)
- **You serve 2-3 distinct personas** → Tiered
- **You're unsure** → Start with Flat-Rate, add tiers later when you understand your customers

## SaaS Metrics — Formulas

| Metric | Formula | What it tells you |
|--------|---------|-------------------|
| **MRR** | Sum of all monthly recurring revenue | Current monthly revenue run rate |
| **ARR** | MRR × 12 | Annualized revenue (use for context, not projection) |
| **ARPU** | Total MRR / total paying customers | Average revenue per customer per month |
| **Churn Rate** | Customers lost in period / customers at start of period | % of customers leaving per month |
| **Revenue Churn** | MRR lost in period / MRR at start of period | % of revenue leaving per month (can differ from customer churn) |
| **LTV** | ARPU × Gross Margin / Monthly Churn Rate | Total revenue expected from one customer over their lifetime |
| **CAC** | Total acquisition spend / new customers acquired | Cost to acquire one customer |
| **LTV:CAC** | LTV / CAC | Return on acquisition investment (target: > 3:1) |
| **Payback Period** | CAC / (ARPU × Gross Margin) | Months to recoup acquisition cost |
| **NRR** | (Starting MRR + expansion - contraction - churn) / Starting MRR × 100 | Net revenue retention — above 100% means growth without new customers |
| **Gross Margin** | (Revenue - COGS) / Revenue | Percentage of revenue that's actual profit after direct costs |

## Unit Economics Template

```
Revenue per customer:     ${ARPU}/mo
Cost to acquire:          ${CAC}
Cost to serve:            ${serving_cost}/mo
  - Hosting:              ${hosting} / {customers} = ${per_customer}
  - Support:              ${support_hours} × ${hourly_rate} / {customers}
  - Third-party APIs:     ${api_cost_per_customer}
  - Transaction fees:     ${ARPU} × {stripe_rate} = ${fees}
Gross margin:             (${ARPU} - ${serving_cost}) / ${ARPU} = {X}%
LTV:                      ${ARPU} × {margin} / {churn} = ${LTV}
LTV:CAC:                  ${LTV} / ${CAC} = {ratio}:1
Payback:                  ${CAC} / (${ARPU} × {margin}) = {months} months
```

## Pricing Psychology

### Anchor Pricing
Present the most expensive tier first (or a "Contact Us" enterprise tier). This makes the middle tier feel reasonable by comparison. The middle tier should be the one you want most people to choose.

### Decoy Effect
If you have two tiers and people cluster on the cheaper one, add a third tier between them that's slightly worse value than the target tier. This pushes people toward the one you want them to pick.

### Price Endings
- **$X9/mo** ($19, $49, $99): signals value/deal — good for SMB, consumer, price-sensitive markets
- **$X0/mo** ($20, $50, $100): signals quality/premium — good for B2B, professional tools
- **$X7/mo** ($17, $47, $97): signals indie/bootstrapped — good for creator/solopreneur tools

### Tier Naming
| Name style | Signal | Example |
|------------|--------|---------|
| Descriptive | Clarity, professional | Free, Starter, Professional, Enterprise |
| Size-based | Growth path | Solo, Team, Business |
| Metaphorical | Brand personality | Seed, Grow, Scale |

Avoid clever-but-confusing names. "What's the difference between Voyager and Explorer?" is a question you don't want.

### Annual vs Monthly
- Annual discount of 15-20% is standard
- Frame as "2 months free" rather than "17% off" — concrete > abstract
- Annual billing reduces churn mechanically (harder to cancel mid-year)
- Improves cash flow: $228 today vs $19/mo over 12 months

## Break-Even Formula

```
Break-even (units) = Fixed Costs / (Price - Variable Cost per Unit)
Break-even (revenue) = Fixed Costs / Gross Margin %
Break-even (months) = Fixed Costs / (MRR - Variable Costs)
```

### Example
- Fixed costs: $500/mo (hosting, tools, subscriptions)
- Price: $29/mo per customer
- Variable cost: $3/mo per customer (Stripe fees, API costs, storage)
- Contribution margin: $29 - $3 = $26/customer
- Break-even: $500 / $26 = **20 customers**

At 4 new customers/month with 5% churn: break-even at month 6.
