# Support Templates Reference

## KB Article Template

```markdown
# How to [Verb] [Noun]

**Summary:** [One sentence that answers the core question.]

**Prerequisites:**
- [ ] [Requirement 1 — e.g., Admin role required]
- [ ] [Requirement 2 — e.g., Pro plan or higher]

## Steps

1. [Action verb] [specific instruction].
   [Screenshot: description of what the user should see]

2. [Action verb] [specific instruction].
   [Screenshot: description of what the user should see]

3. [Action verb] [specific instruction].

4. [Confirm/verify] [expected result].
   [Screenshot: the success state]

## Troubleshooting

**[Problem 1]**
[Cause] → [Fix]. If that doesn't work, [alternative fix].

**[Problem 2]**
[Cause] → [Fix].

**[Problem 3]**
[Cause] → [Fix]. Contact support if this persists.

## Related Articles
- [Related topic 1](link)
- [Related topic 2](link)
- [Related topic 3](link)
```

## FAQ Structure

Group questions into these categories (skip any that don't apply):

| Category | Purpose | Target questions |
|----------|---------|-----------------|
| Getting Started | First-time setup, onboarding | 5-8 |
| Core Features | How the product works | 5-8 |
| Billing & Plans | Pricing, upgrades, refunds | 4-6 |
| Account & Security | Login, passwords, permissions, data | 4-6 |
| Troubleshooting | Common errors, sync issues, workarounds | 4-6 |

**Answer format:**
- First sentence: direct answer to the question
- Second sentence: brief context or explanation
- Third sentence (optional): link to full article or next step

**Question format:**
- Write as the user would ask — conversational, not formal
- Start with "How do I...", "Can I...", "What happens if...", "Why is..."
- Never: "What is the process for..." or "Regarding the..."

## Canned Response Templates

### Bug Report Received
```
Hi {customer_name},

Thanks for reporting this. I can see the issue with {specific_issue} and I'm looking into it now.

I'll update you within {timeline} with what I find. If you have any screenshots or steps to reproduce, that would help me track it down faster.

— {agent_name}
```

### Bug Resolved
```
Hi {customer_name},

Fixed it. {brief_description_of_fix}.

The change is live now — try {specific_action} and let me know if it's working as expected.

— {agent_name}
```

### Feature Request Received
```
Hi {customer_name},

That's a good idea — I've added it to our feature tracker. {brief_reaction_to_the_idea}.

I can't promise a timeline, but I'll let you know if we start working on it.

— {agent_name}
```

### Refund — Eligible
```
Hi {customer_name},

Done — I've issued a full refund of {amount}. It should appear on your statement within 5-10 business days depending on your bank.

Your account has been switched to the free plan. You still have access to your data if you decide to come back.

— {agent_name}
```

### Refund — Not Eligible
```
Hi {customer_name},

I checked your account — unfortunately, the {X}-day refund window has passed (your last payment was on {date}).

Here's what I can do: I'll credit your account for {offer}, so you get the most out of the remaining time. If that doesn't work, let me know and we'll figure something out.

— {agent_name}
```

### Escalation Notice
```
Hi {customer_name},

This one needs a deeper look from our engineering team. I've escalated it with all the details you've shared.

You'll hear back within {timeline}. I'll follow up personally to make sure it doesn't fall through the cracks.

— {agent_name}
```

### Follow-Up (No Response)
```
Hi {customer_name},

Just checking in — were you able to {resolve/complete the action}? If you're still running into issues, I'm happy to help.

If everything's working, no need to reply — I'll close this ticket in 48 hours.

— {agent_name}
```

## Onboarding Email Sequence

### Email 1: Welcome (send immediately)
**Subject:** You're in — here's your first step
**Goal:** Confirm signup, set one clear expectation, one CTA
**Structure:**
- Welcome line (1 sentence, no fluff)
- What they can do now (1 sentence)
- Primary CTA button: [Do the first thing]
- What to expect: "Over the next week, I'll send you 3 short emails to help you get the most out of {product}."

### Email 2: First Action (day 1-2)
**Subject:** Do this first (takes 2 minutes)
**Goal:** Get them to complete the product's core value action
**Structure:**
- "Most people who stick with {product} do {action} in their first session."
- 3-step guide to completing the action
- Screenshot or GIF of the result
- CTA button: [Complete {action}]

### Email 3: Feature Highlight (day 4-5)
**Subject:** The feature most people miss
**Goal:** Show a high-value feature they probably haven't discovered
**Structure:**
- "Did you know you can {feature}?"
- Quick explanation of the value (1-2 sentences)
- How to find it (1-2 steps)
- CTA button: [Try {feature}]

### Email 4: Feedback Request (day 7-10)
**Subject:** Quick question
**Goal:** Learn what's confusing, show you care, catch churn signals
**Structure:**
- "You've been using {product} for a week. How's it going?"
- One specific question: "What's the one thing that's been confusing or frustrating?"
- Reply-to works (not a no-reply address)
- Optional: link to a 2-question survey
- Close: "Seriously — just hit reply. I read every response."
