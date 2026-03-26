# Analytics & Security — Impact Checklist

These two cross-cutting engineering functions are grouped because they share a pattern: both are frequently forgotten until after launch, and both are cheaper to address during development than after.

---

## Analytics

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

---

## Security

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

---

## Effort Estimation (Combined)

| Deliverable | Typical Range |
|------------|--------------|
| Tracking event plan | 0.5-1 day |
| Event implementation | 0.5-1 day per feature area |
| Dashboard creation | 0.5-1 day |
| Security code review | 0.5-2 days |
| Threat model | 0.5-1 day |
| Penetration test | 2-5 days (often outsourced) |
| Secrets audit | 0.5 day |
