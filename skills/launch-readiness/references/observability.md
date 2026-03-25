# Observability Checklist

Observability is how you know what's happening in production without being in the room. Error monitoring (covered separately) is one piece. This file covers the rest: analytics, performance, uptime, and logging.

## Product Analytics

### What to Check

- [ ] Analytics tool integrated (Plausible, PostHog, Mixpanel, Amplitude, etc.)
- [ ] Privacy-compliant (no cookie banner needed if using privacy-first tools like Plausible)
- [ ] Tracking: page views, feature usage, user role distribution
- [ ] Key business events tracked (signup, onboarding complete, first action, subscription)
- [ ] Funnel analysis possible (identify where users drop off)
- [ ] Dashboard accessible (team can check metrics without engineering help)

### Recommendations by Stage

**Pre-launch / MVP**: Plausible or PostHog (self-hosted or cloud). Privacy-friendly, no cookie banner, gives you page views + basic events. 30 minutes to set up.

**Post-10 customers**: PostHog or Mixpanel. Event-based tracking, funnels, cohort analysis, session replays. Half a day to set up properly.

**Post-100 customers**: Consider splitting: Plausible for marketing site analytics + PostHog/Amplitude for product analytics. Different teams look at different data.

### What to Track First

```
1. Page views by role (which features do different roles actually use?)
2. Core action completion (did they finish the main workflow?)
3. Time to first action (how long from signup to first meaningful use?)
4. Error rate by page (which pages are broken for real users?)
5. Session duration (engagement indicator)
```

---

## Performance Budgets

Performance budgets are hard limits on page size, load time, and resource count. If a page exceeds the budget, it's a bug — same as a failing test.

### What to Check

- [ ] Performance budgets defined (even informal targets)
- [ ] Lighthouse CI or equivalent runs periodically
- [ ] Core Web Vitals monitored (LCP < 2.5s, FID < 100ms, CLS < 0.1)
- [ ] Bundle size tracked (Vite bundle analyzer, webpack-bundle-analyzer)
- [ ] No render-blocking resources that could be deferred
- [ ] Images optimized (WebP/AVIF, appropriate sizes, lazy loaded)
- [ ] Fonts: preloaded, subset, with proper `font-display`

### Recommended Budgets

These are starting points — adjust based on your target market and device profile:

```
- First contentful paint (FCP): < 1.5s
- Largest contentful paint (LCP): < 2.5s
- Time to interactive (TTI): < 3.5s
- Total JS bundle: < 250KB gzipped (initial load)
- Total CSS: < 50KB gzipped
- Per-page API calls: < 5 on initial load
- Image payload per page: < 500KB
```

### When to Implement

Performance budgets are P2. Set them up after you have real users and real performance data. Premature optimization before you have traffic is wasted effort. The exception: if your initial bundle is already > 500KB, investigate now — it'll only get worse.

---

## Uptime Monitoring

### What to Check

- [ ] External uptime monitor configured (UptimeRobot, Better Stack, Checkly, etc.)
- [ ] Monitors health endpoint(s): app URL, API endpoint, login page
- [ ] Alert on downtime: email + Slack/Discord/SMS
- [ ] Status page for customers (optional but professional)
- [ ] Response time monitoring (alert if p95 exceeds threshold)

### Minimum Setup

```
1. Sign up for UptimeRobot (free tier: 50 monitors, 5-min interval)
2. Add monitors:
   - https://app.yoursite.com (full page load)
   - https://app.yoursite.com/api/health (API check, if exists)
   - https://yoursite.com (marketing site)
3. Set alerts: email + Slack webhook
4. Optional: status.yoursite.com (Better Stack or Instatus)
```

This takes 10 minutes and immediately tells you when your app goes down — before your customers tell you.

---

## Structured Logging

### What to Check

- [ ] Server logs are structured (JSON format, not console.log strings)
- [ ] Log levels used correctly (error, warn, info, debug)
- [ ] Request ID attached to all logs (traceable per request)
- [ ] User context attached to logs (user ID, org ID — not PII)
- [ ] Logs shipped to a centralized location (not just stdout)
- [ ] Log retention policy defined
- [ ] No sensitive data in logs (passwords, tokens, PII)

### When to Implement

Structured logging is P2-P3. At launch with < 10 customers, `console.log` and Sentry errors are enough. Invest in structured logging when:

- You need to debug issues across multiple services
- You're processing enough requests that searching stdout is impractical
- Compliance requires audit trails

### Recommended Stack

**Simple**: Console.log → Sentry for errors (what you already have)

**Moderate**: Pino (structured JSON logger) → shipped to Logtail/Better Stack

**Full**: Pino → OpenTelemetry → Grafana/Datadog (spans, traces, metrics, logs in one place)

---

## Summary: What to Do When

| Stage          | Analytics                | Performance                | Uptime                    | Logging                  |
| -------------- | ------------------------ | -------------------------- | ------------------------- | ------------------------ |
| Pre-launch     | Plausible/PostHog basic  | Bundle size check          | UptimeRobot free          | console.log + Sentry     |
| 10 customers   | Event tracking + funnels | Lighthouse CI monthly      | Paid monitor, status page | Consider structured      |
| 100 customers  | Full product analytics   | Performance budgets in CI  | SLA monitoring            | Structured + centralized |
| 1000 customers | Dedicated analytics eng  | Real User Monitoring (RUM) | Multi-region checks       | OpenTelemetry            |
