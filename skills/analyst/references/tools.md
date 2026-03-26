# Analytics Tools Reference

## Plausible

- **Type:** Privacy-first web analytics
- **Hosting:** Cloud or self-hosted
- **Script size:** <1KB
- **Cookie-free:** Yes — no consent banner needed
- **Best for:** Marketing sites, landing pages, content sites, GDPR/CCPA compliance
- **Limitations:** Basic event tracking only, no funnels, no session replay, no cohort analysis
- **Pricing:** From $9/mo (cloud), free (self-hosted)

**SvelteKit setup:**
```html
<!-- app.html -->
<script defer data-domain="yourdomain.com" src="https://plausible.io/js/script.js"></script>
```

**Next.js setup:**
```typescript
// next.config.js — add script via next/script in _app.tsx
import Script from 'next/script';
<Script defer data-domain="yourdomain.com" src="https://plausible.io/js/script.js" />
```

## PostHog

- **Type:** Product analytics suite (events, funnels, session replay, feature flags)
- **Hosting:** Cloud or self-hosted (Docker)
- **Best for:** SaaS products, startups wanting one tool, product-led growth
- **Strengths:** Autocapture, session replay, feature flags, A/B testing, funnels — all in one
- **Limitations:** Can get expensive at scale, self-hosting requires maintenance
- **Pricing:** Free up to 1M events/mo, then usage-based

**SvelteKit setup:** `npm install posthog-js` → init in `+layout.svelte` `onMount`
**Next.js setup:** `npm install posthog-js` → init in `_app.tsx` `useEffect` or use `posthog-js/react` provider

## Mixpanel

- **Type:** Event-based product analytics
- **Hosting:** Cloud only
- **Best for:** Mobile apps, B2C with high event volume, cohort analysis, retention curves
- **Strengths:** Powerful segmentation, cohort analysis, retention reports, real-time data
- **Limitations:** No session replay, no feature flags, separate tool for experiments
- **Pricing:** Free up to 20M events/mo (generous), then usage-based

**Setup (universal):** `npm install mixpanel-browser` → init with project token

## Google Analytics 4

- **Type:** Marketing analytics and attribution
- **Hosting:** Cloud only (Google)
- **Best for:** Marketing attribution, SEO tracking, ad campaign measurement, free analytics
- **Strengths:** Free, integrates with Google Ads/Search Console, standard reporting
- **Limitations:** Complex setup, data sampling at scale, privacy concerns, steep learning curve for custom events
- **Pricing:** Free (standard), GA360 for enterprise

**Setup:** Add gtag.js script or use `@analytics/google-analytics` package

## Decision Matrix

| Need | Recommendation | Why |
|------|---------------|-----|
| Privacy-first marketing site | Plausible | No cookies, lightweight, GDPR-safe |
| SaaS product analytics | PostHog | Events + funnels + replay in one tool |
| Mobile app / high-volume B2C | Mixpanel | Best cohort analysis and retention |
| SEO + ad attribution | GA4 | Free, Google ecosystem integration |
| "I don't know yet" | PostHog | Most flexible, generous free tier |

## General Setup Principles

- **Environment gating:** Never track in development. Check `import.meta.env.DEV` or `process.env.NODE_ENV`.
- **Keys in env vars:** Never hardcode project keys. Use `.env` and add the var name to `.env.example`.
- **SPA page tracking:** Disable auto pageview, track manually on route change.
- **User identification:** Call `identify()` after login, never before. Pass user ID + plan + signup date as traits.
- **Event naming:** Use `object_action` format. Lowercase, underscore-separated. Be consistent.
