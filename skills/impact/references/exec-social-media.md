# Social Media — Execution Module

Load this when the impact execution loop needs to create social media content (platform-specific posts, threads, content calendars).

## Workflow

### Modes

**Single Post** (default): One post for a specified platform (or all platforms if unspecified). Use when the task is "write a post", "tweet this", "LinkedIn post."

**Thread Mode**: Multi-post thread for X/Twitter or LinkedIn carousel-style. Use when the task says "thread", "break this down", or the content needs 3+ key points.

**Content Calendar**: 5-7 days of planned posts across platforms. Use when the task is "content calendar", "plan a week", "social strategy."

**Strategy Mode**: Platform selection, content pillars, posting cadence, audience mapping. Use when the task is "social strategy", "what should I post", "help me with social."

If uncertain, default to Single Post for all platforms and offer to expand.

### Step 1: Gather Context

Before writing anything:

1. **Check for product-marketing-context**: look for `.claude/product-marketing-context.md` — if found, extract brand voice, target audience, product positioning, and key messages.
2. **Identify the goal**: awareness / engagement / traffic / conversions / community building
3. **Identify the content type**: launch announcement / feature highlight / educational / behind-the-scenes / customer proof / engagement
4. **Detect platform(s)**: X/Twitter, LinkedIn, Instagram, or all. If unspecified, generate for all three.

Ask clarifying questions ONLY if the topic is genuinely ambiguous. If you can infer from context, do so and state your assumptions.

### Step 2: Write the Content

For each platform, apply these rules:

**X/Twitter**: Lead with a hook. Keep it punchy. Use line breaks for rhythm. No hashtag walls — 1-2 max, only if relevant. Threads: first tweet must stand alone as a banger.

**LinkedIn**: Open with a provocative line or personal story. Use short paragraphs (1-2 sentences). No corporate jargon. End with a question or clear CTA. Skip hashtags or use 3-5 relevant ones at the end.

**Instagram**: Visual-first — describe the ideal image/graphic. Caption: hook line, then value, then CTA. Use 5-15 hashtags grouped at the end. Emojis sparingly and only if brand-appropriate.

For each post, include:
- The post text, ready to copy-paste
- Platform label
- Suggested image/visual (1 line)
- CTA type: link click / comment / share / save

### Step 3: Content Calendar (if applicable)

When generating a calendar:

```markdown
# Content Calendar — [Brand/Product] — Week of [Date]

## Monday — [Content Type]
**Platform(s):** [X, LinkedIn, Instagram]
**Topic:** [topic]
**Hook:** [first line]
**Goal:** [awareness/engagement/traffic]
**Post:** [full text]

## Tuesday — [Content Type]
...
```

Balance the week: no more than 1 promotional post per 4 value posts. Mix content types. Cluster related topics (e.g., launch week = announcement -> feature deep-dive -> behind-the-scenes -> customer story -> recap).

### Step 4: Strategy (if applicable)

When generating a strategy:

```markdown
# Social Strategy — [Brand/Product]

## Audience
- **Primary:** [who, where they hang out, what they care about]
- **Secondary:** [who else]

## Platform Selection
| Platform | Why | Content Focus | Cadence |
|----------|-----|---------------|---------|

## Content Pillars (3-4)
1. **[Pillar]** — [what it covers, why it resonates]

## Posting Cadence
- [Platform]: [X posts/week], best times: [times]

## 30-Day Kickstart
Week 1: [theme]
Week 2: [theme]
Week 3: [theme]
Week 4: [theme]
```

### After Generating

Offer:
1. **Variations?** "Want 3 hook variations for the top post?"
2. **Expand?** "Want a full content calendar for the week around this?"
3. **Adapt?** "Want this adapted for another platform?"

**If the user gives feedback**, revise immediately. Don't defend the original — the user knows their audience better than you do.

## Templates

### Platform Reference

#### X/Twitter

- **Character limit:** 280 per tweet, threads for long-form
- **Thread rules:** First tweet must stand alone. Number threads (1/7) or use a hook + thread marker. Last tweet = CTA or summary. Optimal thread length: 4-8 tweets.
- **Formatting:** Line breaks create visual rhythm. No bold/italic. Use arrows or bullets for lists.
- **Hashtags:** 1-2 maximum. More than that looks spammy. Only use if genuinely discoverable.
- **Media:** Images boost engagement 2-3x. GIFs for personality. Video autoplay catches attention but requires captions.
- **Engagement patterns:** Replies and quote tweets drive reach more than likes. Controversial/contrarian takes get shared. Questions in the last line boost replies.
- **Best posting times:** Weekdays 8-10am, 12-1pm (audience timezone). B2B does well early morning.
- **What works:** Hot takes, concise lessons, before/after, build-in-public updates, data/numbers.
- **What doesn't:** Generic motivational quotes, thread-bait with no substance, hashtag walls.
- **Profile tip:** Pin your best-performing or most relevant tweet. Update monthly.

#### LinkedIn

- **Character limit:** 3,000 per post. First ~210 characters show before "see more" — this is your hook.
- **Formatting:** Short paragraphs (1-2 sentences). Line breaks between every paragraph. Bold text for emphasis (use **bold**). Numbered lists work well.
- **Hashtags:** 3-5 relevant ones at the end, or skip entirely. Never inline.
- **Media:** Document posts (PDF carousels) get highest reach. Native video outperforms links. Avoid external links in post body — put them in first comment.
- **Engagement patterns:** Comments boost reach significantly. Posts that spark professional debate do well. Personal stories outperform corporate updates 3:1.
- **Best posting times:** Tuesday-Thursday, 7-9am or 12pm. Avoid weekends.
- **What works:** Founder stories, lessons learned, counterintuitive business insights, "here's what I'd do differently", data-backed posts.
- **What doesn't:** Humble brags disguised as gratitude, "I'm thrilled to announce" openers, walls of hashtags, reposting without commentary.
- **Algorithm note:** First hour engagement determines reach. Post when your audience is online, not when you finish writing.
- **Pro move:** Reply to every comment within the first hour. Each reply counts as engagement and extends reach.

#### Instagram

- **Caption limit:** 2,200 characters. Only first ~125 characters show in feed — this is your hook.
- **Formatting:** Line breaks for readability. Emojis as bullet points (sparingly). First line is the hook — it shows in the feed preview.
- **Hashtags:** 5-15 relevant ones. Mix broad (#startup) with niche (#SaaSfounder). Place at the end or in the first comment.
- **Content types:** Carousels get highest saves. Reels get highest reach. Single images get least engagement unless striking.
- **Carousel tips:** 7-10 slides optimal. First slide = hook/title. Last slide = CTA. One idea per slide. Consistent visual template.
- **Reels:** 30-60 seconds optimal. Hook in first 3 seconds. Text overlays for silent viewing. Trending audio helps discoverability.
- **Best posting times:** Weekdays 11am-1pm, 7-9pm. Reels: evenings and weekends.
- **What works:** Carousels with tactical tips, behind-the-scenes, relatable founder moments, data visualizations, before/after screenshots.
- **What doesn't:** Stock photos, text-only images, pure sales pitches, inconsistent visual style.
- **Stories:** Use for time-sensitive content, polls, Q&A, behind-the-scenes. Highlights = evergreen story categories.

#### Cross-Platform Rules

- **Never cross-post verbatim.** Each platform has different norms. A LinkedIn post pasted into Twitter looks wrong.
- **CTA placement:** Twitter = last line. LinkedIn = last paragraph. Instagram = "link in bio" or "save this."
- **Posting frequency:** Quality > quantity. 3 good posts/week > 7 mediocre ones.
- **Engagement window:** Reply to every comment in the first 2 hours. This is the highest-leverage activity on any platform.
- **Repurposing flow:** Long-form blog -> LinkedIn article -> Twitter thread -> Instagram carousel -> Individual tweets from thread highlights.
- **Link handling:** Twitter = inline links fine. LinkedIn = link in first comment (algorithm penalizes links in body). Instagram = "link in bio" only.
- **Scheduling:** Batch-create content, schedule ahead. But always be ready to jump on timely opportunities.
- **Analytics check:** Review top-performing posts weekly. Double down on formats and topics that resonate. Kill what doesn't.

### Post Templates by Content Type

#### Launch Announcement

**Structure:** Problem -> Solution -> How it works -> CTA

```
[Hook: the pain point or the unlock]

We just shipped [feature/product].

Here's what it does:
-> [Benefit 1]
-> [Benefit 2]
-> [Benefit 3]

[CTA: try it / link / learn more]
```

**Variations:** Lead with a number ("We spent 3 months building this"), lead with the customer pain ("Tired of X?"), lead with a bold claim ("This replaces your entire X workflow").

#### Feature Highlight

**Structure:** Before/After or "You can now..."

```
[Before]: [how it used to work — the friction]
[After]: [how it works now — the magic]

[1-2 sentences on what changed]

[CTA or "try it"]
```

**Alt format:**
```
You can now [do thing] in [Product].

No more [old painful way].
Just [new easy way].

[Screenshot or demo link]
```

#### Behind-the-Scenes / Building in Public

**Structure:** Story -> Lesson -> Takeaway

```
[What happened — be specific]

[Why it matters or what you learned]

[The takeaway for the reader]

[Optional: what's next]
```

**Tips:** Use real numbers ("took 47 days, not 2 weeks"). Admit mistakes. Show the messy middle, not just the polished result. Screenshots of Slack messages, git logs, or dashboards add authenticity.

#### Educational / Tips

**Structure:** Promise -> Deliver -> Summarize

```
[X] things I wish I knew about [topic]:

1. [Tip] — [1-line explanation]
2. [Tip] — [1-line explanation]
3. [Tip] — [1-line explanation]

[Summary or "which one resonates most?"]
```

**Alt format (single tip):**
```
[Counterintuitive statement about topic]

Here's why:

[Explanation in 2-3 short paragraphs]

[Practical application]
```

#### Customer Proof / Testimonial

**Structure:** Quote -> Context -> Result

```
"[Direct quote from customer]"

[Who they are and what they were trying to solve]

[The measurable result]

[Soft CTA: "see how [Customer] uses [Product]" or link to case study]
```

**Tips:** Real quotes > paraphrased. Specific results > vague praise. "Cut onboarding time from 3 weeks to 4 days" > "really helped us improve."

#### Engagement / Conversation Starter

**Structure:** Question or Hot Take -> Invite Response

```
[Provocative question or bold opinion]

[1-2 sentences of context or your own answer]

[Invitation to respond: "What's yours?" / "Agree or disagree?" / "Drop yours below"]
```

**Types that work:**
- **This or that:** "Notion or Linear for project management?"
- **Unpopular opinion:** "[Contrarian take]. Here's why I think this..."
- **Ask for help:** "Building X, stuck on Y. What would you do?"
- **Poll format:** "How do you handle [X]? A) ... B) ... C) ..."

#### Milestone / Celebration

**Structure:** Number -> Story -> Gratitude -> Forward-look

```
[The milestone — lead with the number]

[Brief story of how you got here — 2-3 sentences]

[What you learned or what surprised you]

[What's next]
```

**Tips:** Share a real number even if it's small. "100 users" is more relatable than "incredible growth." Include a lesson, not just a celebration.

## Principles

**Hook first.** The first line determines if anyone reads the rest. Spend 50% of your effort on the opening. No "Excited to announce..." — start with the value or the tension.

**Platform-native.** LinkedIn is not Twitter with more characters. Instagram is not LinkedIn with pictures. Different audiences, different norms, different formats. Respect each platform's culture.

**Value over promotion.** 80% useful/educational/entertaining, 20% promotional. People follow accounts that make them smarter, not accounts that sell to them.

**Consistent voice.** Every post should sound like the same person wrote it. Match the brand's established tone from product-marketing-context. When no context exists, default to: knowledgeable, direct, slightly informal, zero corporate speak.

## Example

**Task**: "Write a launch announcement for our new referral program"
**Assumption:** SaaS product, target audience is existing customers and potential users.

### X/Twitter

> Your customers are your best salespeople.
>
> We just launched referral rewards:
> -> Your friend gets 1 month free
> -> You get $20 credit per referral
> -> No limit on referrals
>
> Takes 30 seconds to share your link.
>
> [product.com/referrals]

**Visual:** Clean graphic showing the referral flow (share -> sign up -> both get rewarded)
**CTA:** Link click

### LinkedIn

> We spent $4,000 on ads last month. Our best 12 customers brought in 31 signups for $0.
>
> The math was obvious. So we built a referral program.
>
> Here's how it works:
>
> Share your unique link with anyone who'd benefit from [Product]. When they sign up, they get their first month free. You get $20 in credit — no cap.
>
> We're betting that people who get recommended by a friend stay longer, engage more, and complain less than people who click an ad.
>
> Early data says we're right.
>
> If you're already using [Product], your referral link is in your dashboard right now. -> [product.com/referrals]

**Visual:** Screenshot of the referral dashboard with link + stats
**CTA:** Link click + comment ("Tag someone who'd love this")

### Instagram

> Your network = your superpower
>
> We just launched something our community has been asking for: a referral program that actually rewards you.
>
> Here's the deal:
> - Share your unique link
> - Your friend gets 1 month FREE
> - You get $20 credit (no limits)
>
> The best part? It takes 30 seconds. Link in bio.
>
> #SaaS #ReferralProgram #StartupLife #GrowthHacking #ProductLaunch

**Visual:** Carousel — Slide 1: "Your customers are your best marketing channel" / Slide 2: How it works (3 steps) / Slide 3: "Start referring -> link in bio"
**CTA:** Link in bio + save for later
