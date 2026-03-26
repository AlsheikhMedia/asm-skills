# Analytics Frameworks Reference

## SaaS KPI Framework

The 8 metrics every SaaS founder should track:

| KPI | Definition | How to Calculate | Check Frequency |
|-----|-----------|-----------------|-----------------|
| **MRR** | Monthly Recurring Revenue | Sum of all active subscription amounts | Daily |
| **Churn Rate** | % of customers lost per period | Churned customers / Start-of-period customers | Weekly |
| **LTV** | Lifetime Value per customer | ARPU / Churn Rate | Monthly |
| **CAC** | Customer Acquisition Cost | Total sales+marketing spend / New customers | Monthly |
| **LTV:CAC** | Unit economics health | LTV / CAC (target: >3:1) | Monthly |
| **Activation Rate** | % of signups who reach "aha moment" | Activated users / Total signups | Weekly |
| **NPS** | Net Promoter Score | % Promoters - % Detractors | Quarterly |
| **Revenue Churn** | $ lost from downgrades + cancellations | Lost MRR / Start-of-period MRR | Weekly |

**What "activated" means:** Define the single action that correlates with retention. For Slack it's "sent 2000 messages as a team." For Dropbox it's "uploaded 1 file." Find yours by comparing retained vs. churned users.

## AARRR Funnel (Pirate Metrics)

| Stage | Question | Example Events | Key Metric |
|-------|----------|---------------|------------|
| **Awareness** | Do people find us? | `page_viewed`, `ad_clicked` | Unique visitors |
| **Acquisition** | Do they sign up? | `user_signed_up` | Signup rate |
| **Activation** | Do they get value? | `user_activated`, `onboarding_completed` | Activation rate |
| **Revenue** | Do they pay? | `plan_upgraded`, `payment_completed` | Conversion to paid |
| **Referral** | Do they tell others? | `referral_sent`, `invite_accepted` | Viral coefficient |

**How to use:** Measure each stage. Fix the worst drop-off first. Improving activation from 20% to 40% has more impact than improving awareness by 10%.

## Dashboard Layout Standard

```
┌─────────┬─────────┬─────────┬─────────┐
│  KPI 1  │  KPI 2  │  KPI 3  │  KPI 4  │  ← KPI cards with sparkline + % change
├─────────┴─────────┴─────────┴─────────┤
│                                        │
│         Primary Trend Chart            │  ← Main metric over time (30d default)
│         (with comparison period)       │
│                                        │
├────────────────────┬───────────────────┤
│   Funnel Chart     │  Segment Table    │  ← Conversion funnel + breakdown by segment
│                    │                   │
└────────────────────┴───────────────────┘
```

**Rules:**
- Top-level KPIs: 4-6 max. Each with current value, previous period, % change, sparkline.
- Trend chart: default to 30 days. Allow 7d / 30d / 90d toggle. Always show comparison period (dotted line).
- Detail table: sortable by any column. Filterable by segment (plan, country, source).
- No pie charts. Ever. Use bar charts for comparisons, line charts for trends.

## A/B Test Specification

```markdown
**Hypothesis:** If we [specific change], then [metric] will [direction] by [amount] because [reasoning based on data/observation].

**Primary metric:** [one metric — the thing you're optimizing for]
**Secondary metrics:** [2-3 guardrail metrics that must not degrade]

**Sample size:** Calculate from:
  - Baseline conversion rate: [X]%
  - Minimum detectable effect (MDE): [Y]% relative improvement
  - Statistical significance: 95% (α = 0.05)
  - Power: 80% (β = 0.20)

**Duration:** Total sample needed / Daily traffic = Days to run
  - Minimum: 7 days (capture weekly patterns)
  - Maximum: 30 days (avoid novelty effects fading)

**Kill criteria:** Stop if guardrail metric degrades by more than [X]%.
```

**Common mistakes:** Running tests too short (weekly cycles matter). Peeking at results and stopping early. Testing too many variants at once. No hypothesis = no learning even if you "win."

## Event Naming Convention

**Format:** `object_action`

| Object | Actions | Examples |
|--------|---------|----------|
| `user` | `signed_up`, `logged_in`, `activated`, `churned` | `user_signed_up` |
| `page` | `viewed`, `scrolled`, `exited` | `page_viewed` |
| `feature` | `used`, `discovered`, `abandoned` | `feature_used` |
| `plan` | `viewed`, `upgraded`, `downgraded`, `cancelled` | `plan_upgraded` |
| `onboarding` | `started`, `step_completed`, `completed`, `skipped` | `onboarding_step_completed` |
| `referral` | `sent`, `clicked`, `accepted`, `rewarded` | `referral_sent` |
| `support` | `requested`, `resolved`, `rated` | `support_requested` |
| `email` | `sent`, `opened`, `clicked`, `unsubscribed` | `email_opened` |

**Rules:**
- Always lowercase, underscore-separated
- Past tense for completed actions (`signed_up` not `sign_up`)
- Properties carry the specifics: `feature_used { feature_name: "export", duration_ms: 3400 }`
- Never put variable data in event names: `feature_used` with `feature_name` property, NOT `export_feature_used`
