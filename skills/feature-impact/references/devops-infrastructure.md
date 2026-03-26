# DevOps/Infrastructure — Impact Checklist

When a feature, task, or initiative affects DevOps or Infrastructure, use this checklist to identify specific deliverables, dependencies, and risks.

## What to Check

### Deployment
- [ ] Deployment config changes needed (environment variables, secrets)
- [ ] New service or worker to deploy
- [ ] Database migration to run (before or during deploy?)
- [ ] Feature flag to configure (enabled/disabled per environment)
- [ ] Deployment order matters (backend before frontend? Migration before app?)
- [ ] Zero-downtime deployment possible or maintenance window needed?
- [ ] Rollback procedure documented and tested

### CI/CD Pipeline
- [ ] New CI steps needed (test, build, lint for new code)
- [ ] Pipeline config updated for new service/route
- [ ] Build time impact assessed (stays under 10 minutes?)
- [ ] New secrets/env vars added to CI environment

### Environment Management
- [ ] Staging environment updated (matches production config)
- [ ] Environment variables synchronized across environments
- [ ] Third-party service sandboxes configured (payment, email, auth)
- [ ] Seed data works in all environments

### Monitoring & Observability
- [ ] Error monitoring configured for new code paths
- [ ] Health check endpoint updated (if new service)
- [ ] Alerting rules added (errors, latency, availability)
- [ ] Log levels appropriate (no sensitive data in logs)
- [ ] Performance baseline established (before/after comparison)

### External Service Provisioning
- [ ] Third-party accounts created (error tracking, email, payments, analytics)
- [ ] API keys/DSNs obtained and stored in secrets manager
- [ ] Sandbox/test environment configured for third-party services
- [ ] Rate limits and quotas checked (free tier sufficient or paid needed?)
- [ ] Service SLA reviewed (uptime guarantees, support response time)

### Infrastructure Changes
- [ ] DNS changes needed
- [ ] SSL/TLS certificates needed
- [ ] CDN config changes
- [ ] Database scaling or config changes

## Typical Dependencies

**DevOps needs FROM:**

| Department | What | Why |
|-----------|------|-----|
| Development | Deployment artifacts, environment requirements, config changes | Can't deploy what isn't built |
| Product | Launch timeline, rollout strategy, feature flag decisions | Need to know when and how to deploy |
| Security | Security review sign-off, compliance requirements | Can't deploy without security clearance |

**DevOps PRODUCES for:**

| Department | What | Why |
|-----------|------|-----|
| Development | Working environments, CI pipeline, deployment capability | Dev needs infrastructure to build on |
| QA/Testing | Test environments, staging parity, feature flag states | QA needs environments to test in |
| Analytics | Monitoring data, performance metrics | Analytics needs operational data |
| All departments | Production availability, deployment execution | Everyone depends on things being live |

## Common Deliverables by Initiative Type

### New Feature
- [ ] Environment variables configured (staging + production)
- [ ] Feature flag created and configured
- [ ] Deployment pipeline verified
- [ ] Monitoring/alerting for new code paths
- [ ] Rollback plan tested

### Infrastructure Sprint
- [ ] Service provisioning (databases, hosting, CDN)
- [ ] CI/CD pipeline creation or modification
- [ ] Environment parity verification
- [ ] Migration runner setup
- [ ] Seed data pipeline

### Third-Party Integration
- [ ] API keys/credentials securely stored
- [ ] Sandbox vs. production environment separation
- [ ] Webhook endpoints configured
- [ ] Rate limiting and retry logic
- [ ] Fallback behavior if service is down

## Effort Estimation Guide

| Deliverable | Typical Range |
|------------|--------------|
| Environment variable setup | 0.5-1 hour |
| Feature flag configuration | 0.5-1 hour |
| CI pipeline modification | 0.5-1 day |
| New service deployment setup | 1-3 days |
| Database provisioning | 0.5-1 day |
| DNS + SSL setup | 0.5-1 day |
| Monitoring + alerting setup | 0.5-1 day |
| Full environment provisioning | 2-5 days |

## Common Mistakes

- No staging test before production deploy (staging exists for a reason)
- Missing environment variables in production (works in staging, breaks in prod)
- No rollback plan (or rollback plan not tested)
- Running migrations as part of app startup (should be a separate deploy step)
- Feature flags with no cleanup plan (zombie flags accumulate)
- Monitoring added after launch (can't see problems that happened during rollout)
- Hardcoded URLs or credentials in config (breaks across environments)
