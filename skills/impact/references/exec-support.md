# Support — Execution Module

Load this when the impact execution loop needs to create customer support infrastructure (KB articles, FAQs, canned responses, onboarding emails).

## Workflow

### Step 1: Detect Mode

Classify the request into one of these modes:

1. **KB Article** — a specific how-to or troubleshooting guide
2. **FAQ** — a comprehensive Q&A set covering the product
3. **Canned Responses** — reply templates for common support scenarios
4. **Help Center** — a full help center structure (categories, article hierarchy)
5. **Onboarding Sequence** — post-signup email/in-app guidance
6. **Escalation Workflow** — rules for when/how to escalate issues

If unclear, ask one question. If you can infer from context, state your assumption and proceed.

### Step 2: Gather Context

Before writing anything:

1. **Scan the project** for product context: README, feature lists, route files, schema definitions, component names, existing docs
2. **Check for existing support content**: `docs/`, `help/`, `support/`, `content/`, any `.md` files with user-facing language
3. **Identify the product's core flows**: signup, onboarding, main value action, billing, settings
4. **Note the tech stack**: this affects troubleshooting steps (e.g., "clear browser cache" vs "restart the app")
5. **Check for brand context**: `.claude/product-marketing-context.md` for tone and terminology

Use what you find. Don't ask the user to describe features you can read from the codebase.

### Step 3: Generate Content

#### KB Article Mode

Title must be action-oriented ("How to [verb] [noun]"). Include: one-sentence summary that answers the question upfront -> prerequisites -> numbered steps with `[Screenshot: description]` placeholders -> 2-3 troubleshooting items -> related articles.

#### FAQ Mode

Scan all features and user flows from the codebase. Generate questions a real user would ask — not marketing fluff. Group by category (Getting Started, Core Features, Billing & Plans, Account & Security, Troubleshooting), 5-8 per category, 20-30 total. Each answer: direct answer first sentence, then 1-2 sentences of context.

#### Canned Responses Mode

Generate responses for: bug reports (received/investigating/resolved/can't reproduce), feature requests (received/planned/declined), refunds (eligible/not eligible), account issues (locked out/billing/cancellation), and general (greeting/acknowledgment/escalation/follow-up). Each: greeting -> acknowledgment -> action -> next steps -> sign-off.

#### Help Center Mode

Propose 4-6 top-level categories, 5-10 article titles each. Mark priority: P1 (before launch), P2 (within 2 weeks), P3 (when asked). Suggest writing order based on expected ticket volume.

#### Onboarding Sequence Mode

Generate 4 emails: Welcome (immediate, one CTA) -> First Action (day 1-2, core value action) -> Feature Highlight (day 4-5, hidden gem) -> Feedback Request (day 7-10, ask what's confusing).

#### Escalation Workflow Mode

Define tiers: T1 self-serve (0 min) -> T2 canned response (< 2hr) -> T3 investigation (< 24hr) -> T4 founder/dev (< 48hr). Include routing rules and criteria for each tier.

### Step 4: Output

Format all output in clean Markdown, ready to be saved directly as documentation files. Use consistent heading levels, and include file path suggestions (e.g., `docs/help/getting-started/how-to-sign-up.md`).

```markdown
# [Article Title / FAQ / Help Center Structure]

<!-- Mode: [detected mode] -->
<!-- Product: [product name from context] -->
<!-- Generated: [date] -->

[Content based on mode]
```

### Step 5: After Generation

Ask:

1. **Save it?** "Want me to save these to your docs/ folder?"
2. **More coverage?** "I identified [N] more topics that should have articles. Want me to generate those?"
3. **Tone check?** "These are written in [detected tone]. Want me to adjust?"

## Templates

### KB Article Template

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
[Cause] -> [Fix]. If that doesn't work, [alternative fix].

**[Problem 2]**
[Cause] -> [Fix].

**[Problem 3]**
[Cause] -> [Fix]. Contact support if this persists.

## Related Articles
- [Related topic 1](link)
- [Related topic 2](link)
- [Related topic 3](link)
```

### FAQ Structure

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

### Canned Response Templates

#### Bug Report Received
```
Hi {customer_name},

Thanks for reporting this. I can see the issue with {specific_issue} and I'm looking into it now.

I'll update you within {timeline} with what I find. If you have any screenshots or steps to reproduce, that would help me track it down faster.

— {agent_name}
```

#### Bug Resolved
```
Hi {customer_name},

Fixed it. {brief_description_of_fix}.

The change is live now — try {specific_action} and let me know if it's working as expected.

— {agent_name}
```

#### Feature Request Received
```
Hi {customer_name},

That's a good idea — I've added it to our feature tracker. {brief_reaction_to_the_idea}.

I can't promise a timeline, but I'll let you know if we start working on it.

— {agent_name}
```

#### Refund — Eligible
```
Hi {customer_name},

Done — I've issued a full refund of {amount}. It should appear on your statement within 5-10 business days depending on your bank.

Your account has been switched to the free plan. You still have access to your data if you decide to come back.

— {agent_name}
```

#### Refund — Not Eligible
```
Hi {customer_name},

I checked your account — unfortunately, the {X}-day refund window has passed (your last payment was on {date}).

Here's what I can do: I'll credit your account for {offer}, so you get the most out of the remaining time. If that doesn't work, let me know and we'll figure something out.

— {agent_name}
```

#### Escalation Notice
```
Hi {customer_name},

This one needs a deeper look from our engineering team. I've escalated it with all the details you've shared.

You'll hear back within {timeline}. I'll follow up personally to make sure it doesn't fall through the cracks.

— {agent_name}
```

#### Follow-Up (No Response)
```
Hi {customer_name},

Just checking in — were you able to {resolve/complete the action}? If you're still running into issues, I'm happy to help.

If everything's working, no need to reply — I'll close this ticket in 48 hours.

— {agent_name}
```

### Onboarding Email Sequence

#### Email 1: Welcome (send immediately)
**Subject:** You're in — here's your first step
**Goal:** Confirm signup, set one clear expectation, one CTA
**Structure:**
- Welcome line (1 sentence, no fluff)
- What they can do now (1 sentence)
- Primary CTA button: [Do the first thing]
- What to expect: "Over the next week, I'll send you 3 short emails to help you get the most out of {product}."

#### Email 2: First Action (day 1-2)
**Subject:** Do this first (takes 2 minutes)
**Goal:** Get them to complete the product's core value action
**Structure:**
- "Most people who stick with {product} do {action} in their first session."
- 3-step guide to completing the action
- Screenshot or GIF of the result
- CTA button: [Complete {action}]

#### Email 3: Feature Highlight (day 4-5)
**Subject:** The feature most people miss
**Goal:** Show a high-value feature they probably haven't discovered
**Structure:**
- "Did you know you can {feature}?"
- Quick explanation of the value (1-2 sentences)
- How to find it (1-2 steps)
- CTA button: [Try {feature}]

#### Email 4: Feedback Request (day 7-10)
**Subject:** Quick question
**Goal:** Learn what's confusing, show you care, catch churn signals
**Structure:**
- "You've been using {product} for a week. How's it going?"
- One specific question: "What's the one thing that's been confusing or frustrating?"
- Reply-to works (not a no-reply address)
- Optional: link to a 2-question survey
- Close: "Seriously — just hit reply. I read every response."

## Principles

**Answer first, explain second.** The user is stuck. The first sentence of every article and FAQ answer must directly address what they came for. Bury the background.

**Screenshots beat paragraphs.** Mark every step where a visual would help. A 5-step guide with screenshot placeholders is worth more than a 20-step wall of text.

**Write for the frustrated user.** They're not reading for fun. Short sentences. Clear actions. No jargon without explanation. No "simply" or "just" — if it were simple, they wouldn't need the article.

**One article, one topic.** Don't combine "how to sign up" with "how to reset your password." If a user searches for one, they shouldn't wade through the other.

**Canned doesn't mean robotic.** Templates should sound like a competent human who cares, not a corporation that doesn't. Include placeholders for personalization: `{customer_name}`, `{specific_issue}`, `{timeline}`.

## Example

**Task**: "Generate an FAQ for our SaaS app"
Context scan reveals: task management app with projects, team members, Kanban boards, time tracking, Stripe billing, Google SSO.

```markdown
# FAQ — TaskFlow

## Getting Started

**How do I create my first project?**
Click "New Project" from your dashboard, name it, and choose a template (Kanban, List, or Timeline). Invite team members now or later from Project Settings -> Members.

**Can I import tasks from another tool?**
Yes. Settings -> Import -> upload a CSV. We support Trello, Asana, and Jira. Column mapping is automatic — review the preview before confirming.

## Billing & Plans

**What's included in the free plan?**
Up to 3 projects, 5 team members, 1 GB storage. Time tracking and Kanban included. Integrations and reporting require a paid plan.

**Can I get a refund?**
Full refund within 14 days. After that, we credit the remaining period.

## Account & Security

**How do I reset my password?**
"Forgot Password" on login page -> enter email -> reset link within 2 minutes. Google SSO users: sign in with Google instead.

## Troubleshooting

**Tasks aren't syncing across devices.**
Hard refresh (Ctrl+Shift+R / Cmd+Shift+R). If it persists, check status.taskflow.com.

<!-- Full FAQ would continue with 20-30 questions across 5 categories -->
```
