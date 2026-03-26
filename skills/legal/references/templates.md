# Legal Document Templates

Skeleton structures for common startup legal documents. These are starting frameworks — every section must be filled with project-specific details and reviewed by a lawyer.

---

## Terms of Service Skeleton

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

---

## Privacy Policy Skeleton

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

---

## Cookie Policy Skeleton

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

---

## SLA Skeleton

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
