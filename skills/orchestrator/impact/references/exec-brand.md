# Brand — Execution Module

> **Expertise:** You are a brand director / chief brand officer with 20+ years of domain mastery in brand strategy, positioning, and creative direction. This team has zero juniors. Every deliverable must be the absolute best — no generic positioning, no templated messaging, no borrowed brand voice. If the task demands specialist knowledge (naming linguistics, visual identity systems, cultural semiotics, luxury branding), bring in that expert. The bar: seasoned brand leaders review your output and say "WOW."

Load this when the impact execution loop needs to create brand identity (positioning, messaging framework, tone of voice, visual identity).

## Workflow

### Step 1: Detect Mode

Classify the request:

1. **Full Brand Guide** — comprehensive: positioning + messaging + tone + visual identity + story
2. **Positioning** — who you're for, what you do differently, and why it matters
3. **Tone of Voice** — how the brand sounds across all touchpoints
4. **Messaging Framework** — headline, subheadline, pillars, proof points
5. **Visual Identity Brief** — colors, typography, logo direction, photography style
6. **Naming** — brand name, product name, or feature naming exploration
7. **Brand Story** — origin, mission, vision, values narrative

If the task asks for a "brand guide," run Full mode. For specific requests, run that mode only.

### Step 2: Gather Context

Before building anything:

1. **Scan the project** for product context: README, landing page copy, about page, existing marketing materials
2. **Check for existing brand context**: `.claude/product-marketing-context.md`, brand guidelines, style guide, design tokens
3. **Look at the product itself**: UI copy, error messages, onboarding text — these reveal the current (often accidental) brand voice
4. **Check competitors**: if there's competitive analysis docs, use them. If not, ask what the founder considers the 2-3 closest alternatives.
5. **Identify the audience**: who uses this, what's their job title, what problem brings them to this product

Ask for missing context only when critical. If you can infer from codebase and docs, state your assumptions and proceed.

### Step 3: Build the Brand

#### Full Brand Guide Mode

Run in order — each section feeds the next: Positioning -> Messaging -> Tone of Voice -> Brand Story -> Visual Identity Brief.

#### Individual Modes

Use the frameworks below. Each mode:

- **Positioning**: target persona -> category -> differentiator -> positioning statement -> anti-positioning (who this is NOT for)
- **Messaging**: headline (6-10 words, benefit-first) -> subheadline (15-25 words) -> 3 pillars (claim + proof + CTA) -> objection reframes
- **Tone of Voice**: rate 4 dimensions (formal<->casual, serious<->playful, respectful<->irreverent, enthusiastic<->matter-of-fact), "We are / We are not" + examples + banned words
- **Visual Identity**: primary color (hex + rationale) -> secondary colors -> typography -> logo direction (concept, not design) -> photography style -> UI implications
- **Naming**: criteria -> 10-15 candidates (descriptive/metaphorical/invented/compound) -> score -> top 3
- **Brand Story**: origin (founder's frustration) -> mission -> vision -> 3-5 values with behaviors

### Step 4: Output

Format as a single Markdown document ready to be saved as a brand reference file.

```markdown
# Brand Guide — [Product Name]

<!-- Generated: [date] -->

[Sections based on mode — structured per templates above]
```

### Step 5: After Generation

Ask:

1. **Save it?** "Want me to save this as `.claude/brand-guide.md` for other skills to reference?"
2. **Apply it?** "Want me to audit your current copy against this tone of voice?"
3. **Go deeper?** "Want me to expand any section — e.g., write 10 headline variations?"

## Templates

### Positioning Template

```
For [target customer — specific persona, not "businesses"]
who [struggle or unmet need — what's painful today],
[Product] is a [category — what shelf it sits on]
that [key benefit — what changes for them].
Unlike [1-2 named alternatives],
we [differentiator — what's uniquely true about you].
```

#### Positioning Checklist
- [ ] Target is specific enough that you could find these people in a room
- [ ] Category is one the customer already understands (don't invent one)
- [ ] Benefit is about the customer, not about your product
- [ ] Differentiator is verifiable — a competitor couldn't honestly say the same thing
- [ ] Anti-positioning is defined — you know who this is NOT for

#### Category Rules
- Use a category the customer already shops in: "project management" not "work orchestration"
- If you're creating a new category, you need a massive marketing budget. You probably don't have one.
- Add a qualifier to own a niche: "project management for freelancers" > "project management"

### Messaging Framework

#### Structure

```markdown
**Headline** (6-10 words)
Benefit-first. What changes for the customer?
No jargon. No cleverness that sacrifices clarity.

**Subheadline** (15-25 words)
Expands on the how. Adds specificity.
Can include the product category if the headline doesn't.

**Pillar 1: [Theme]**
Claim: One sentence promise
Proof: Feature, metric, or testimonial that backs it up
CTA: Specific action the reader can take

**Pillar 2: [Theme]**
(same structure)

**Pillar 3: [Theme]**
(same structure)
```

#### Headline Rules
- Lead with benefit, not feature: "Get paid faster" not "Automated invoicing"
- Be specific: "Save 5 hours a week" not "Save time"
- Avoid superlatives: "best", "fastest", "most powerful" — nobody believes them
- Test: if a competitor could say the same thing, it's not specific enough

#### Pillar Selection
Choose 3 pillars that are:
1. **Distinct**: each pillar covers a different value dimension
2. **Provable**: each has a concrete proof point (not just a claim)
3. **Resonant**: each addresses a real pain point or desire of the target persona

Common pillar patterns:
- Product capability -> Outcome -> Trust/credibility
- Save time -> Save money -> Reduce stress
- Easy to start -> Powerful to use -> Grows with you

### Tone Matrix

Rate the brand on 4 dimensions. Each sits on a spectrum.

#### Dimension 1: Formal <-> Casual
| Formal | Casual |
|--------|--------|
| "We appreciate your patience" | "Thanks for hanging in there" |
| Third person, complete sentences | First/second person, fragments OK |
| B2B enterprise, legal, finance | B2C, tools for creators, SMB |

#### Dimension 2: Serious <-> Playful
| Serious | Playful |
|---------|---------|
| "Secure your data with encryption" | "Your secrets are safe with us" |
| Factual, no humor, direct | Light touches of wit, personality |
| Security products, healthcare, B2B | Consumer apps, creative tools |

#### Dimension 3: Respectful <-> Irreverent
| Respectful | Irreverent |
|------------|------------|
| "We understand the challenge" | "Yeah, that old way is broken" |
| Acknowledges complexity, empathetic | Calls out industry BS, contrarian |
| Regulated industries, diverse audiences | Startups disrupting incumbents |

#### Dimension 4: Enthusiastic <-> Matter-of-fact
| Enthusiastic | Matter-of-fact |
|-------------|----------------|
| "We're thrilled to announce!" | "New feature: dark mode." |
| Excited, energetic, exclamation marks | Calm, confident, period. |
| Community-driven, early-stage | Developer tools, productivity |

#### Writing the "We Are / We Are Not"
For each dimension, write:
- **We are**: the positive trait (e.g., "direct")
- **We are not**: the negative extreme (e.g., "blunt or rude")
- **Example**: one sentence in the right tone

### Brand Story Structure

#### Origin
Why does this product exist? What frustrated the founder enough to build it?
- Not: "We saw a gap in the market"
- Yes: "I ran a 20-person cleaning crew and spent every Sunday night rebuilding the schedule because someone called in sick. I built CleanOps because nobody should dread Sundays."

#### Mission
What do you do every day? One sentence.
- Format: "We [verb] [who] [outcome]"
- Example: "We help cleaning business owners spend less time on admin and more time growing."

#### Vision
Where is this headed? What does the world look like if you succeed?
- Format: "A world where [outcome]"
- Example: "A world where running a cleaning business is as professional and streamlined as running a tech company."

#### Values (3-5)
Each value must have a behavior — what it looks like in practice.

| Value | Behavior | Anti-behavior |
|-------|----------|---------------|
| Clarity | We explain things in plain language. No jargon. | We don't hide behind buzzwords. |
| Reliability | We ship when we say we will. Features work on day one. | We don't launch half-broken and call it "beta." |
| Respect | We respect our users' time. No dark patterns, no unnecessary steps. | We don't optimize for our metrics at the user's expense. |

### Visual Identity Brief Structure

#### Primary Color
- Hex code + rationale
- What emotion/association it creates
- How it differentiates from competitors (check their brand colors first)

#### Secondary Colors
- 2-3 colors that complement the primary
- Usage rules: backgrounds, accents, CTAs, text
- Ensure sufficient contrast ratios (WCAG AA minimum: 4.5:1 for text)

#### Typography
- **Heading font**: personality-carrying, used sparingly
- **Body font**: highly legible, clean, works at small sizes
- Rationale: why these fonts match the brand personality
- Common safe pairings: Inter + Inter, Space Grotesk + Inter, DM Sans + DM Sans

#### Logo Direction
Describe the concept — don't design it. Include:
- Type: wordmark / lettermark / symbol / combination
- Feeling: what someone should think when they see it
- Avoid: what it should NOT look like

#### Photography / Illustration Style
- Subject matter: what's in the images
- Lighting: natural / studio / dramatic
- Color treatment: vibrant / muted / desaturated
- People: real vs. illustrated, diverse representation, candid vs. posed
- What to avoid: stock photo cliches, specific examples

#### UI Implications
How the visual identity manifests in the product:
- Button styles: rounded vs. sharp, filled vs. outlined
- Spacing: generous (premium feel) vs. dense (power user)
- Iconography: line vs. filled, rounded vs. sharp
- Motion: subtle vs. expressive

## Principles

**Positioning is a decision, not a description.** "We help businesses be more productive" is a description. "We're the project management tool for freelancers who hate project management tools" is a position. Choose who you're for and own it — trying to be for everyone means you're for no one.

**Tone of voice is how you say it, not what you say.** Two brands can communicate the same feature — "End-to-end encryption" — and sound completely different. One says "Your data is protected by military-grade encryption." The other says "We can't read your stuff. Nobody can." Same fact, different personality.

**Consistency beats creativity.** A mediocre brand applied consistently across every touchpoint — site, emails, error messages, support replies, social — builds more trust than a brilliant brand applied randomly. The goal is recognition, not admiration.

**Brand is not a logo.** It's the promise you make and keep. Every interaction either reinforces or undermines it. The best brand work happens in the mundane: the loading state message, the invoice email subject line, the 404 page.

## Example

**Task**: "Create a brand guide for our project management SaaS"
Context scan reveals: scheduling and job management app for cleaning companies, 5-50 employees, competes with Jobber and Housecall Pro.

```markdown
# Brand Guide — CleanOps

## Positioning

**For** cleaning business owners with 5-50 employees
**who** waste hours on scheduling, invoicing, and chasing crews,
**CleanOps** is a job management platform
**that** turns chaos into a system that runs without you babysitting it.
**Unlike** Jobber and Housecall Pro (built for all home services),
**we** are built exclusively for cleaning — every feature assumes recurring visits, walk-throughs, and supply tracking.

### Who This Is NOT For
- Solo cleaners: too much tool for the job
- General contractors: features are cleaning-specific
- Enterprise (100+): no multi-location or union scheduling

## Messaging

**Headline:** Run your cleaning business, not your schedule
**Subheadline:** Scheduling, crew dispatch, client communication, and invoicing — so you can grow without drowning in admin.

| Pillar | Claim | Proof |
|--------|-------|-------|
| Built for Cleaning | Every feature designed for how cleaning businesses work | Recurring visits, walk-through checklists, supply tracking |
| Crews Stay on Track | Your crew knows where to go without calling you | Mobile app, route optimization, photo verification |
| Get Paid Faster | Invoice the moment a job is done, automatically | Auto-invoicing, online payment, recurring billing |

## Tone of Voice

| Dimension | We Are | We Are Not |
|-----------|--------|------------|
| Formal <-> Casual | Friendly, plain-spoken | Stiff, corporate |
| Serious <-> Playful | Light when appropriate | Goofy, pun-heavy |
| Respectful <-> Irreverent | Acknowledging hard work | Dismissive of struggle |
| Enthusiastic <-> Matter-of-fact | Clear, confident, no hype | "AMAZING!!" |

**Error — wrong:** "Oopsie! Something went wrong. Our bad!"
**Error — right:** "That didn't save. Check your connection and try again."

## Visual Identity Brief

**Primary:** #1B6B4A (forest green) — clean, natural, stands out from competitor blues
**Secondary:** #F5F0E8 (warm off-white), #2D3436 (charcoal) for text
**Type:** Inter (headings + body) — clean, modern, legible
**Logo:** Wordmark with subtle checkmark — signals "done, handled"
**Photography:** Real crews at work, not stock. Diverse teams, natural lighting.
```
