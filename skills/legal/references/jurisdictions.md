# Jurisdiction Reference

Key legal requirements by jurisdiction for startup legal documents. This is a reference for document generation — not legal advice.

---

## UAE

### Federal Data Protection
- **Law**: Federal Decree-Law No. 45/2021 on the Protection of Personal Data
- **Effective**: January 2, 2022 (enforcement began March 2023)
- **Scope**: Processing of personal data of UAE residents
- **Key requirements**:
  - Lawful basis required (consent, contract, legal obligation, vital interest, public interest)
  - Data subject rights: access, rectification, erasure, restriction, portability
  - Cross-border transfer restrictions — adequate protection required
  - Data breach notification to UAE Data Office "without undue delay"
  - Data Protection Officer may be required for certain processing activities

### DIFC (Dubai International Financial Centre)
- **Law**: DIFC Data Protection Law No. 5 of 2020
- **Scope**: Entities operating within DIFC
- **Key additions**: More closely aligned with GDPR, includes right to object to automated decision-making
- **Commissioner**: DIFC Commissioner of Data Protection

### ADGM (Abu Dhabi Global Market)
- **Law**: ADGM Data Protection Regulations 2021
- **Scope**: Entities operating within ADGM
- **Similar to**: GDPR framework with ADGM-specific registration requirements

### E-Commerce
- **Law**: Federal Law No. 1/2006 on Electronic Commerce and Transactions
- **Requires**: Clear terms of service, pricing transparency, cancellation rights for online purchases

### Consumer Protection
- **Law**: Federal Law No. 15/2020 on Consumer Protection
- **Key**: 14-day cooling-off period for online purchases (with exceptions for digital goods/services)

---

## United States

### No Federal Privacy Law
- No comprehensive federal data protection law (as of 2026)
- Sector-specific: HIPAA (health), FERPA (education), COPPA (children), GLBA (financial)

### California — CCPA/CPRA
- **Law**: California Consumer Privacy Act (as amended by CPRA)
- **Scope**: Businesses with CA customers meeting revenue/data thresholds
- **Key requirements**:
  - "Do Not Sell or Share My Personal Information" link required
  - Right to know, delete, correct, and port data
  - Right to opt out of sale/sharing of personal information
  - 45-day response window for consumer requests
  - Privacy policy must disclose categories of data collected, purposes, and third parties
  - No dark patterns in opt-out flows

### CAN-SPAM
- **Scope**: Commercial email to US recipients
- **Key requirements**:
  - Clear "From" line, subject line not deceptive
  - Physical postal address required in email
  - Opt-out mechanism, honored within 10 business days
  - No purchased email lists without consent

### Other State Laws
- Virginia (VCDPA), Colorado (CPA), Connecticut (CTDPA) — similar to CCPA with variations
- **Safe approach**: If you comply with CCPA, you largely comply with other state laws

### Terms of Service (US-specific)
- Arbitration clauses and class action waivers are generally enforceable
- Section 230 protections for user-generated content platforms
- DMCA safe harbor requires designated agent and takedown process

---

## European Union (GDPR)

### General Data Protection Regulation
- **Scope**: Processing data of EU/EEA residents, regardless of company location
- **Key requirements**:

#### Consent
- Must be freely given, specific, informed, and unambiguous
- Pre-ticked boxes are NOT valid consent
- Must be as easy to withdraw as to give
- Separate consent for each purpose

#### Lawful Basis (choose one per processing activity)
- Consent, contract performance, legal obligation, vital interests, public task, legitimate interest
- Document which basis applies to each data processing activity

#### Data Subject Rights
- Access (copy of data, 30-day response)
- Rectification (correct inaccurate data)
- Erasure ("right to be forgotten")
- Restriction of processing
- Data portability (machine-readable format)
- Object to processing (especially direct marketing — must stop immediately)
- Not be subject to automated decision-making with legal effects

#### Data Protection Officer (DPO)
- Required if: public authority, core activity is large-scale monitoring, or large-scale processing of special category data
- Most startups do NOT need a DPO initially
- [REVIEW NEEDED: Assess based on actual processing activities]

#### Data Breach Notification
- 72 hours to notify supervisory authority (if risk to rights)
- "Without undue delay" to notify affected individuals (if high risk)

#### International Data Transfers
- Adequate countries: listed by EU Commission (includes UK, Japan, South Korea, etc.)
- Standard Contractual Clauses (SCCs) for transfers to non-adequate countries (US, UAE)
- Binding Corporate Rules for intra-group transfers

#### Records of Processing
- Maintain written records of all processing activities
- Required for companies with 250+ employees OR high-risk processing
- Good practice for all companies regardless

---

## Common Requirements Across All Jurisdictions

### Data Breach Notification
- All three jurisdictions require notification of significant data breaches
- Timeframes vary: 72 hours (GDPR), "without undue delay" (UAE), varies by state (US)
- **Best practice**: Notify within 72 hours universally — satisfies the strictest requirement

### User Rights
- All jurisdictions grant users some form of: access, correction, deletion
- Response timeframes: 30 days (GDPR, UAE), 45 days (CCPA)
- **Best practice**: Implement a single rights-request flow with 30-day SLA

### Transparency
- All jurisdictions require clear disclosure of what data is collected and why
- Privacy policy must be easily accessible (footer link, signup flow)
- Must be written in clear, understandable language (not legalese)

### Children's Data
- GDPR: parental consent for under 16 (member states can lower to 13)
- US COPPA: parental consent for under 13
- UAE: additional protections for minors
- **Best practice**: Do not knowingly collect data from under 16, include statement in privacy policy

### Multi-Jurisdiction Approach
When operating across jurisdictions:
1. Start with GDPR as the baseline (strictest)
2. Add CCPA-specific requirements (Do Not Sell link, 45-day window)
3. Add UAE-specific requirements (UAE Data Office notification, Arabic language consideration)
4. Flag jurisdiction-specific sections clearly in the document
