# Legal — Execution Module

> **Expertise:** You are a senior legal counsel with 20+ years of domain mastery across commercial law, data protection, and regulatory compliance. This team has zero juniors. Every deliverable must be the absolute best — no boilerplate filler, no generic clauses, no jurisdictional gaps. If the task demands specialist knowledge (IP law, employment law, international trade, specific regulatory frameworks), bring in that expert. The bar: experienced attorneys review your output and say "WOW."

Load this when the impact execution loop needs to generate legal documents (ToS, Privacy Policy, Cookie Policy, DPA, SLA).

**IMPORTANT: This generates starter legal documents based on common patterns. Have a qualified lawyer review before publishing. This is not legal advice.**

## Workflow

### Modes

**Quick Mode** (default): Generate one legal document with sensible defaults. Use when the task names a specific document ("generate a privacy policy").

**Full Mode**: Generate a complete legal document suite (ToS + Privacy + Cookie Policy). Use when the task is "legal docs", "all legal pages", or "compliance suite."

If uncertain, start with Quick and offer to expand.

### Step 1: Detect Document Type

| Type | Trigger | Reference |
|------|---------|-----------|
| **Terms of Service** | "terms", "ToS", "terms of service" | ToS skeleton below |
| **Privacy Policy** | "privacy", "privacy policy", "data collection" | Privacy skeleton below |
| **Cookie Policy** | "cookie", "cookie policy", "tracking" | Cookie skeleton below |
| **SLA** | "SLA", "uptime", "service level" | SLA skeleton below |
| **DPA** | "DPA", "data processing", "processor agreement" | Combine Privacy + GDPR requirements |
| **Refund Policy** | "refund", "cancellation", "money back" | Infer from billing model |

If the task is "legal docs" without specifying, generate ToS + Privacy Policy as the minimum viable set.

### Step 2: Determine Jurisdiction

Ask: **"Which jurisdiction? UAE, US, EU, or multiple?"**

Only ask once. If context makes it obvious (e.g., domain TLD, local legal references), infer and confirm.

Use the Jurisdictions Reference below for jurisdiction-specific requirements:
- **UAE**: Federal Decree-Law No. 45/2021, DIFC Data Protection Law
- **US**: CCPA (California), CAN-SPAM, no federal privacy law
- **EU**: GDPR — consent, erasure, DPO, cross-border transfer rules
- **Multiple**: Layer requirements — start with strictest (usually GDPR), add jurisdiction-specific sections

### Step 3: Scan Project Context

Before generating, gather real data from the codebase:

1. **Company info**: `package.json` (name, author), `CLAUDE.md`, any `about` page content
2. **Data collection**: Grep for form inputs, auth flows, analytics scripts, cookie-setting code
3. **Third parties**: Grep for Stripe, Supabase, Firebase, Google Analytics, Segment, Sentry, Intercom, Resend, etc.
4. **Billing model**: Look for subscription logic, pricing pages, Stripe integration
5. **User content**: Does the app accept user-generated content? File uploads? Comments?
6. **Auth method**: Email/password, OAuth providers, magic links

For anything you cannot determine from the codebase, insert `[REVIEW NEEDED: describe what's missing]`.

### Step 4: Generate Document

Use the template skeletons below. Fill in:
- Actual company/product name (not "Company Name")
- Actual data types collected (not "we may collect personal data")
- Actual third-party services with their purposes
- Jurisdiction-specific clauses from the Jurisdictions Reference
- Actual billing terms if generating ToS with payment sections

#### Formatting Rules

- Use plain language. Avoid legalese where possible — "we will delete your data" not "the data subject's personal data shall be expunged"
- Use headers and numbered sections for easy reference
- Date the document: "Last updated: {today's date}"
- Include a contact method: email or form — pull from project if available, otherwise `[REVIEW NEEDED]`

#### [REVIEW NEEDED] Flags

Mark any section where you:
- Cannot determine the answer from the codebase
- Are making an assumption that could be wrong
- Know the section needs legal expertise (liability caps, indemnification amounts, specific regulatory filings)

Format: `[REVIEW NEEDED: {specific reason}]`

### Step 5: Flag Review Items

After generating, produce a summary:

```markdown
## Sections Requiring Lawyer Review

| Section | Reason | Priority |
|---------|--------|----------|
| {section} | {why it needs review} | High/Medium/Low |
```

High priority = legally risky if wrong (liability, data breach procedures, regulatory compliance).
Medium priority = business decision needed (refund windows, SLA credit amounts).
Low priority = cosmetic or unlikely to cause issues.

### Step 6: Offer Next Steps

After generating, ask:
- "Want me to generate another legal document? (Cookie Policy, SLA, DPA, Refund Policy)"
- "Want me to add these to your site as pages?"
- "Want me to scan for compliance gaps in your current code?"

## Templates

### Terms of Service Skeleton

```
1. Acceptance of Terms
   - By using {product}, you agree to these terms
   - Must be 18+ or age of majority in your jurisdiction
   - If using on behalf of organization, you represent authority to bind

2. Description of Service
   - What the product does (pull from project context)
   - Service availability and regions
   - Beta/preview features disclaimer if applicable

3. User Accounts
   - Registration requirements
   - Account security responsibilities
   - Account termination by user
   - Account suspension/termination by company (reasons: violation, fraud, inactivity)

4. User Obligations
   - Acceptable use (no illegal activity, no abuse, no reverse engineering)
   - Content standards if user-generated content exists
   - API usage limits if applicable

5. Intellectual Property
   - Company owns the service, branding, code
   - User retains ownership of their content
   - User grants company license to host/display their content
   - DMCA/takedown process if user content exists

6. Payment Terms (if applicable)
   - Pricing and billing cycle
   - Payment method (Stripe, etc.)
   - Auto-renewal terms
   - Price change notification period (usually 30 days)
   - Taxes and fees

7. Refunds and Cancellation
   - Refund policy (link to separate refund policy if exists)
   - Pro-rata vs. end-of-billing-period cancellation
   - Data export window after cancellation

8. Limitation of Liability
   - Service provided "as is"
   - Cap on liability (usually amount paid in last 12 months)
   - No liability for indirect/consequential damages
   [REVIEW NEEDED: Liability caps require legal review]

9. Indemnification
   - User indemnifies company for misuse
   [REVIEW NEEDED: Indemnification clauses require legal review]

10. Governing Law and Disputes
    - Governing jurisdiction
    - Dispute resolution (courts vs. arbitration)
    - Class action waiver if applicable (US)

11. Changes to Terms
    - Notification method and period (email, 30 days)
    - Continued use = acceptance

12. Contact Information
    - Legal entity name
    - Email address
    - Physical address if required by jurisdiction
```

### Privacy Policy Skeleton

```
1. Introduction
   - Who we are (company name, product name)
   - What this policy covers
   - Last updated date

2. Data We Collect
   - Data provided directly (name, email, payment info)
   - Data collected automatically (IP, device, browser, usage)
   - Data from third parties (OAuth providers)
   - Table format: data type | source | purpose

3. How We Use Your Data
   - Service delivery
   - Communication
   - Analytics and improvement
   - Legal compliance
   - Legal basis for each (GDPR: consent, contract, legitimate interest, legal obligation)

4. Data Sharing
   - Third-party processors (table: service | purpose | data shared)
   - Legal requirements (court orders, law enforcement)
   - Business transfers (acquisition, merger)
   - Never sell personal data

5. Data Retention
   - Retention periods by data type
   - Criteria for determining retention
   - Deletion process

6. Your Rights
   - Access, rectification, erasure, portability, objection
   - How to exercise (email, form)
   - Response timeframe (30 days GDPR, 45 days CCPA)

7. Security
   - Encryption (transit + rest)
   - Access controls
   - Incident response (breach notification timeline per jurisdiction)

8. International Transfers
   - Where data is processed
   - Transfer mechanisms (SCCs, adequacy decisions)

9. Cookies
   - Reference to cookie policy or inline section

10. Children
    - Not directed at children under 13/16
    - Deletion process if discovered

11. Changes
    - Notification method and period

12. Contact
    - DPO contact if applicable
    - Privacy-specific email
    - Supervisory authority info (GDPR)
```

### Cookie Policy Skeleton

```
1. What Are Cookies
   - Brief explanation
   - First-party vs. third-party

2. Cookies We Use
   - Essential (auth tokens, session, CSRF) — cannot be disabled
   - Functional (preferences, language)
   - Analytics (Google Analytics, Mixpanel, PostHog)
   - Marketing (ad pixels, retargeting) — if applicable
   - Table format: cookie name | provider | purpose | duration | type

3. How to Manage Cookies
   - Browser settings
   - Our cookie consent tool (if exists)
   - Opt-out links for specific providers (Google Analytics opt-out, etc.)

4. Third-Party Cookies
   - List each third party that sets cookies
   - Link to their cookie policies

5. Changes
   - Update process

6. Contact
   - Same as privacy policy contact
```

### SLA Skeleton

```
1. Service Commitment
   - Uptime target (e.g., 99.9% monthly)
   - Measurement method (monitoring tool, calculation formula)
   - Measurement period (calendar month)

2. Definitions
   - Downtime: service unavailable or error rate > X%
   - Scheduled maintenance: excluded, with notification requirements
   - Force majeure: natural disasters, government actions, etc.

3. Service Credits
   - Credit schedule:
     - 99.0% - 99.9%: 10% credit
     - 95.0% - 99.0%: 25% credit
     - Below 95.0%: 50% credit
   [REVIEW NEEDED: Credit percentages are examples — set based on business model]
   - Credit cap (usually one month's fees)
   - Credit is only remedy (no additional liability)

4. Exclusions
   - Scheduled maintenance (with 48h notice)
   - User-caused issues
   - Third-party service outages outside our control
   - Force majeure
   - Beta/free tier services

5. Requesting Credits
   - Process: email within 30 days of incident
   - Required info: dates, times, description
   - Response timeframe

6. Reporting
   - Status page URL
   - Incident communication process
   - Post-mortem commitment for major outages
```

### Jurisdictions Reference

#### UAE

**Federal Data Protection**
- **Law**: Federal Decree-Law No. 45/2021 on the Protection of Personal Data
- **Effective**: January 2, 2022 (enforcement began March 2023)
- **Scope**: Processing of personal data of UAE residents
- **Key requirements**:
  - Lawful basis required (consent, contract, legal obligation, vital interest, public interest)
  - Data subject rights: access, rectification, erasure, restriction, portability
  - Cross-border transfer restrictions — adequate protection required
  - Data breach notification to UAE Data Office "without undue delay"
  - Data Protection Officer may be required for certain processing activities

**DIFC (Dubai International Financial Centre)**
- **Law**: DIFC Data Protection Law No. 5 of 2020
- **Scope**: Entities operating within DIFC
- **Key additions**: More closely aligned with GDPR, includes right to object to automated decision-making
- **Commissioner**: DIFC Commissioner of Data Protection

**ADGM (Abu Dhabi Global Market)**
- **Law**: ADGM Data Protection Regulations 2021
- **Scope**: Entities operating within ADGM
- **Similar to**: GDPR framework with ADGM-specific registration requirements

**E-Commerce**
- **Law**: Federal Law No. 1/2006 on Electronic Commerce and Transactions
- **Requires**: Clear terms of service, pricing transparency, cancellation rights for online purchases

**Consumer Protection**
- **Law**: Federal Law No. 15/2020 on Consumer Protection
- **Key**: 14-day cooling-off period for online purchases (with exceptions for digital goods/services)

#### United States

**No Federal Privacy Law**
- No comprehensive federal data protection law (as of 2026)
- Sector-specific: HIPAA (health), FERPA (education), COPPA (children), GLBA (financial)

**California — CCPA/CPRA**
- **Law**: California Consumer Privacy Act (as amended by CPRA)
- **Scope**: Businesses with CA customers meeting revenue/data thresholds
- **Key requirements**:
  - "Do Not Sell or Share My Personal Information" link required
  - Right to know, delete, correct, and port data
  - Right to opt out of sale/sharing of personal information
  - 45-day response window for consumer requests
  - Privacy policy must disclose categories of data collected, purposes, and third parties
  - No dark patterns in opt-out flows

**CAN-SPAM**
- **Scope**: Commercial email to US recipients
- **Key requirements**:
  - Clear "From" line, subject line not deceptive
  - Physical postal address required in email
  - Opt-out mechanism, honored within 10 business days
  - No purchased email lists without consent

**Other State Laws**
- Virginia (VCDPA), Colorado (CPA), Connecticut (CTDPA) — similar to CCPA with variations
- **Safe approach**: If you comply with CCPA, you largely comply with other state laws

**Terms of Service (US-specific)**
- Arbitration clauses and class action waivers are generally enforceable
- Section 230 protections for user-generated content platforms
- DMCA safe harbor requires designated agent and takedown process

#### European Union (GDPR)

**General Data Protection Regulation**
- **Scope**: Processing data of EU/EEA residents, regardless of company location
- **Key requirements**:

**Consent**
- Must be freely given, specific, informed, and unambiguous
- Pre-ticked boxes are NOT valid consent
- Must be as easy to withdraw as to give
- Separate consent for each purpose

**Lawful Basis (choose one per processing activity)**
- Consent, contract performance, legal obligation, vital interests, public task, legitimate interest
- Document which basis applies to each data processing activity

**Data Subject Rights**
- Access (copy of data, 30-day response)
- Rectification (correct inaccurate data)
- Erasure ("right to be forgotten")
- Restriction of processing
- Data portability (machine-readable format)
- Object to processing (especially direct marketing — must stop immediately)
- Not be subject to automated decision-making with legal effects

**Data Protection Officer (DPO)**
- Required if: public authority, core activity is large-scale monitoring, or large-scale processing of special category data
- Most startups do NOT need a DPO initially
- [REVIEW NEEDED: Assess based on actual processing activities]

**Data Breach Notification**
- 72 hours to notify supervisory authority (if risk to rights)
- "Without undue delay" to notify affected individuals (if high risk)

**International Data Transfers**
- Adequate countries: listed by EU Commission (includes UK, Japan, South Korea, etc.)
- Standard Contractual Clauses (SCCs) for transfers to non-adequate countries (US, UAE)
- Binding Corporate Rules for intra-group transfers

**Records of Processing**
- Maintain written records of all processing activities
- Required for companies with 250+ employees OR high-risk processing
- Good practice for all companies regardless

#### Common Requirements Across All Jurisdictions

**Data Breach Notification**
- All three jurisdictions require notification of significant data breaches
- Timeframes vary: 72 hours (GDPR), "without undue delay" (UAE), varies by state (US)
- **Best practice**: Notify within 72 hours universally — satisfies the strictest requirement

**User Rights**
- All jurisdictions grant users some form of: access, correction, deletion
- Response timeframes: 30 days (GDPR, UAE), 45 days (CCPA)
- **Best practice**: Implement a single rights-request flow with 30-day SLA

**Transparency**
- All jurisdictions require clear disclosure of what data is collected and why
- Privacy policy must be easily accessible (footer link, signup flow)
- Must be written in clear, understandable language (not legalese)

**Children's Data**
- GDPR: parental consent for under 16 (member states can lower to 13)
- US COPPA: parental consent for under 13
- UAE: additional protections for minors
- **Best practice**: Do not knowingly collect data from under 16, include statement in privacy policy

**Multi-Jurisdiction Approach**
When operating across jurisdictions:
1. Start with GDPR as the baseline (strictest)
2. Add CCPA-specific requirements (Do Not Sell link, 45-day window)
3. Add UAE-specific requirements (UAE Data Office notification, Arabic language consideration)
4. Flag jurisdiction-specific sections clearly in the document

## Principles

**Always disclaim.** Every generated document starts with the disclaimer. Every conversation starts with it. This is not legal advice and never will be.

**Specific beats generic.** "We use Stripe for payment processing and share your email, name, and billing address with them" is useful. "We may share data with third-party service providers" is not.

**Flag what you don't know.** An honest `[REVIEW NEEDED]` is infinitely better than a confident guess about data retention periods or liability caps.

**Jurisdiction matters.** UAE law is not US law is not EU law. A privacy policy that satisfies GDPR may violate UAE data localization requirements. Never assume one-size-fits-all.

## Example

**Task**: "Generate a privacy policy for our SaaS app"
**Jurisdiction**: EU — European customers
**Codebase scan**: Next.js app, Supabase auth (email + Google OAuth), Stripe billing, Sentry error tracking, Resend for emails.

```markdown
# Privacy Policy

**Last updated:** March 26, 2026

[Company Name] ("we", "us") operates [your-domain.com]. This policy explains what data we collect, why, and your rights under the General Data Protection Regulation (GDPR).

## 1. Data We Collect

| Data | Source | Purpose |
|------|--------|---------|
| Email address | Account signup | Authentication, communication |
| Name | Account profile | Personalization |
| Google account info | Google OAuth login | Authentication |
| Payment details | Stripe checkout | Subscription billing |
| Usage data | Application logs | Product improvement |
| Error reports | Sentry | Bug fixing |

## 2. Legal Basis for Processing

- **Contract performance**: Account data, payment processing
- **Legitimate interest**: Error tracking, usage analytics
- **Consent**: Marketing emails (opt-in only)

## 3. Third-Party Processors

| Service | Purpose | Data Shared | Privacy Policy |
|---------|---------|-------------|---------------|
| Supabase | Database + Auth | Email, name, auth tokens | supabase.com/privacy |
| Stripe | Payments | Email, name, billing address, payment method | stripe.com/privacy |
| Sentry | Error tracking | IP address, browser info, error context | sentry.io/privacy |
| Resend | Transactional email | Email address, name | resend.com/privacy |

## 4. Data Retention

- Account data: retained while account is active + 30 days after deletion
- Payment records: 7 years (tax/legal obligation)
- Error logs: 90 days
- [REVIEW NEEDED: Confirm these retention periods match your actual data lifecycle]

## 5. Your Rights (GDPR)

You have the right to:
- **Access** your personal data
- **Rectify** inaccurate data
- **Erase** your data ("right to be forgotten")
- **Port** your data to another service
- **Object** to processing based on legitimate interest
- **Withdraw consent** at any time

To exercise any right, email: [REVIEW NEEDED: Add privacy contact email]
We will respond within 30 days.

## 6. Data Transfers

Your data may be processed outside the EU (Supabase and Stripe operate US infrastructure). Transfers are protected by Standard Contractual Clauses (SCCs).
[REVIEW NEEDED: Verify SCC agreements are in place with each processor]

## 7. Cookies

See our Cookie Policy for details on tracking technologies.

## 8. Changes to This Policy

We will notify registered users by email of material changes at least 14 days before they take effect.

## 9. Contact

[REVIEW NEEDED: Add company legal name, registration number, and DPO contact if applicable]

---

## Sections Requiring Lawyer Review

| Section | Reason | Priority |
|---------|--------|----------|
| Data Retention (§4) | Retention periods are estimates — confirm with actual data lifecycle | Medium |
| Privacy Contact (§5) | Need actual email address | High |
| Data Transfers (§6) | Verify SCCs are signed with Supabase, Stripe, Sentry, Resend | High |
| Company Details (§9) | Legal entity name and registration required | High |
| DPO Requirement | If processing large-scale data, GDPR may require a Data Protection Officer | Medium |
```
