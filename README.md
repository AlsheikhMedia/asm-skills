# ASM Skills

Make Claude Code an expert at the things you actually need done -- launching products, writing copy, optimizing funnels, coordinating across departments. Install a skill once, and it just works.

13 skills by [AlSheikh Media](https://alsheikhmedia.com). Built from shipping real SaaS, not theory.

## Quick Start

```bash
# Install any skill
claude install github:AlsheikhMedia/asm-skills/skills/<tier>/<skill-name>
```

Three good starting points:

```bash
# Your virtual team -- analyzes impact, then executes across 11 departments
claude install github:AlsheikhMedia/asm-skills/skills/orchestrator/impact

# Checks if your SaaS is actually ready to launch (12 domains, brutally honest)
claude install github:AlsheikhMedia/asm-skills/skills/infrastructure/launch-readiness

# Writes marketing copy that sounds like you, not a robot
claude install github:AlsheikhMedia/asm-skills/skills/direct-tools/copywriting
```

Once installed, just talk to Claude Code normally. Skills activate automatically when they match what you're doing.

## Skills

### Orchestrator

| Skill | What it solves | Try saying... |
| --- | --- | --- |
| [impact](skills/orchestrator/impact/) | You need to understand the ripple effects of a decision across your whole org -- and then actually execute on it. Impact analyzes, plans, and does the work across 11 departments. | *"What's the impact of adding live chat?"* |

### Infrastructure

| Skill | What it solves | Try saying... |
| --- | --- | --- |
| [launch-readiness](skills/infrastructure/launch-readiness/) | You're about to launch but aren't sure what you've missed. Audits 12 domains -- from error monitoring to feature flags -- and tells you exactly what needs fixing, in priority order. Can also bootstrap a new project from scratch. | *"Am I ready to launch?"* |
| [save](skills/infrastructure/save/) | You're ending a session and want to pick up where you left off tomorrow. Saves context to memory, commits your work, confirms before pushing. | *"Save progress"* |
| [chain](skills/infrastructure/chain/) | You have multi-step workflows you repeat -- deploy checks, weekly audits, release prep. Chain runs them as an automated sequence with pause points. | *"Run the post-deploy chain"* |
| [chain-create](skills/infrastructure/chain-create/) | You want to define those repeatable workflows. Creates and edits chain definitions. | *"Create a new workflow chain"* |

### Direct Tools -- Marketing

| Skill | What it solves | Try saying... |
| --- | --- | --- |
| [copywriting](skills/direct-tools/copywriting/) | You need marketing copy that converts. Writes or rewrites copy for any page type using proven frameworks (PAS, AIDA, 4Ps). | *"Write copy for our pricing page"* |
| [marketing-ideas](skills/direct-tools/marketing-ideas/) | You're stuck on how to grow. Draws from 139 strategies matched to your stage, budget, and goals. | *"Marketing ideas for early-stage SaaS"* |
| [marketing-psychology](skills/direct-tools/marketing-psychology/) | You want copy that works on a deeper level. 70+ mental models -- anchoring, loss aversion, social proof -- with guidance on when and how to apply each one ethically. | *"How can I use psychology to improve signups?"* |
| [product-marketing-context](skills/direct-tools/product-marketing-context/) | You're tired of re-explaining your product to every marketing skill. Set this up once, and every other marketing skill already knows your positioning, audience, and voice. | *"Set up marketing context"* |
| [programmatic-seo](skills/direct-tools/programmatic-seo/) | You want organic traffic at scale. Generates SEO pages from templates and data -- directories, comparisons, location pages. 12 playbooks. | *"Build comparison pages for our competitors"* |
| [seo-audit](skills/direct-tools/seo-audit/) | Your organic traffic is underperforming. Diagnoses technical SEO, on-page issues, content quality, and AI search readiness. | *"Audit our site's SEO"* |

### Direct Tools -- CRO

| Skill | What it solves | Try saying... |
| --- | --- | --- |
| [cro-funnel](skills/direct-tools/cro-funnel/) | Users are dropping off somewhere in your funnel. Covers every stage: landing page, forms, signup, onboarding, popups, and paywall. | *"Optimize our signup funnel"* |
| [page-cro](skills/direct-tools/page-cro/) | A specific page isn't converting. Analyzes value prop, headline, CTA, trust signals, and structure, then suggests A/B tests. | *"Why isn't our landing page converting?"* |

## The Impact Skill

Impact is the flagship. Where other skills handle one job, Impact coordinates across your entire organization.

Tell it about a feature, initiative, or change, and it will:

- **Analyze** which departments are affected and map the dependency chain
- **Plan** prioritized deliverables with cycle detection so nothing gets stuck in loops
- **Execute** the actual work through 11 specialized modules:

| Module | What it does |
| --- | --- |
| Product | Writes specs, user stories, acceptance criteria |
| Engineering | Builds features, sets up infrastructure |
| Design | Creates UI/UX designs and prototypes |
| QA | Defines test plans, writes test cases |
| Tech Writer | Produces documentation, guides, changelogs |
| Legal | Drafts policies, terms, compliance docs |
| Social Media | Creates posts and content calendars |
| Analyst | Sets up tracking, dashboards, metrics |
| Support | Builds help docs, templates, escalation flows |
| Finance | Models pricing, revenue impact, cost analysis |
| Brand | Crafts positioning, messaging, identity guidelines |

Impact runs modules in parallel when possible, manages state across sessions, and supports cross-department triggers -- when one module's output feeds into another's input.

```bash
claude install github:AlsheikhMedia/asm-skills/skills/orchestrator/impact
```

## Install Methods

### Claude Code CLI (recommended)

```bash
claude install github:AlsheikhMedia/asm-skills/skills/<tier>/<skill-name>
```

Replace `<tier>` with `orchestrator`, `infrastructure`, or `direct-tools`. Replace `<skill-name>` with the skill directory name.

### Manual

```bash
git clone https://github.com/AlsheikhMedia/asm-skills.git
cp -r asm-skills/skills/<tier>/<skill-name> .claude/skills/
```

### From .skill file

Download from [Releases](https://github.com/AlsheikhMedia/asm-skills/releases), then:

```bash
claude install ./<skill-name>.skill
```

## What Are Claude Code Skills?

Skills are instruction files that teach Claude Code how to be an expert at something specific. When you install a skill, it lives in your project's `.claude/skills/` directory as a markdown file. Claude Code reads it automatically when the context matches -- no slash commands, no configuration.

Each skill contains checklists, frameworks, and decision trees that Claude follows to produce structured output. Think of them as giving Claude a detailed playbook for a domain you care about.

Skills are just files. You can read them, edit them, and version them alongside your code.

## Contributing

PRs welcome. Each skill lives in `skills/<tier>/<skill-name>/` with a `SKILL.md` entry point and optional `references/`, `scripts/`, `assets/` directories.

See the [skill format spec](https://code.claude.com/docs/en/skills) for structure details.

## License

MIT -- see [LICENSE](LICENSE). The `cro-funnel` skill is adapted from [AgentKits Marketing](https://github.com/aitytech/agentkits-marketing) (MIT).
