# ASM Skills

Production-grade skills for [Claude Code](https://claude.ai/code) by [AlSheikh Media](https://alsheikhmedia.com).

Born from shipping real SaaS products — not theory. Each skill encodes the checklists, patterns, and strategies we use in production.

## Quick Start

```bash
# Install any skill with one command
claude install github:AlsheikhMedia/asm-skills/skills/<skill-name>
```

**Most popular starting points:**

```bash
# Audit your SaaS project across 12 domains
claude install github:AlsheikhMedia/asm-skills/skills/launch-readiness

# Map cross-team impact before building a feature
claude install github:AlsheikhMedia/asm-skills/skills/feature-impact

# Write conversion-focused marketing copy
claude install github:AlsheikhMedia/asm-skills/skills/copywriting
```

Once installed, just describe what you need in Claude Code. The skills trigger automatically based on context.

## Skills

### Infrastructure & Operations

| Skill | What it does | Try saying... |
| --- | --- | --- |
| [launch-readiness](skills/launch-readiness/) | Audits your SaaS project across 12 domains: error monitoring, CI/CD, migrations, staging, design system, page specs, testing, seed data, security, observability, feature flags. Produces a gap report with prioritized fixes. Also bootstraps new projects from scratch. | *"Am I ready to launch?"* |
| [feature-impact](skills/feature-impact/) | Maps which departments a feature touches, what each needs to deliver, dependency chains between them, risks if skipped, and a phased execution order with parallel tracks. Works with any org structure. | *"What's the impact of adding live chat?"* |
| [save](skills/save/) | End-of-session saver — updates project memory, commits changes with a clear message, and asks before pushing. Keeps context across sessions. | *"Save progress"* |

### Workflow

| Skill | What it does | Try saying... |
| --- | --- | --- |
| [chain](skills/chain/) | Runs predefined workflow chains — multi-step sequences that execute skills in order with optional pause points between steps. | *"Run the post-deploy chain"* |
| [chain-create](skills/chain-create/) | Creates or edits workflow chains. Saves definitions to `.claude/chains.json` for the chain runner to use. | *"Create a new workflow chain"* |

### Marketing & SEO

| Skill | What it does | Try saying... |
| --- | --- | --- |
| [copywriting](skills/copywriting/) | Writes, rewrites, or improves marketing copy for any page type. Uses proven frameworks (PAS, AIDA, 4Ps) with reference libraries for headline formulas and natural transitions. | *"Write copy for our pricing page"* |
| [marketing-ideas](skills/marketing-ideas/) | 139 proven marketing strategies organized by category — content, community, partnerships, paid, product-led, and more. Matches ideas to your stage, budget, and goals. | *"Give me marketing ideas for early-stage SaaS"* |
| [marketing-psychology](skills/marketing-psychology/) | 70+ mental models applied to marketing — anchoring, loss aversion, social proof, commitment bias, and more. Explains when and how to use each ethically. | *"How can I use psychology to improve signups?"* |
| [product-marketing-context](skills/product-marketing-context/) | Creates a reusable product context doc (`.claude/product-marketing-context.md`) that other marketing skills reference. Set it up once, and every marketing skill knows your positioning, audience, and voice. | *"Set up marketing context"* |
| [programmatic-seo](skills/programmatic-seo/) | Builds SEO-driven pages at scale using templates and data — directory pages, comparison pages, location pages, glossaries. 12 playbooks for different page types. | *"Build comparison pages for our competitors"* |
| [seo-audit](skills/seo-audit/) | Diagnoses SEO issues across on-page, technical, and content quality. Includes AI content detection patterns and AEO/GEO (answer engine optimization) guidance. | *"Audit our site's SEO"* |

### CRO (Conversion Rate Optimization)

| Skill | What it does | Try saying... |
| --- | --- | --- |
| [cro-funnel](skills/cro-funnel/) | Full-funnel CRO covering every stage: page optimization, form design, signup flow, onboarding activation, popup/modal design, and paywall/upgrade screens. Each stage has its own framework. | *"Optimize our signup funnel"* |
| [page-cro](skills/page-cro/) | Single-page conversion optimization with A/B test experiment ideas. Analyzes value prop, headline, CTA, trust signals, and page structure for any marketing page. | *"Why isn't our landing page converting?"* |

## Install

### Claude Code (recommended)

```bash
claude install github:AlsheikhMedia/asm-skills/skills/<skill-name>
```

### Manual

```bash
git clone https://github.com/AlsheikhMedia/asm-skills.git
cp -r asm-skills/skills/<skill-name> .claude/skills/
```

### From .skill file

Download from [Releases](https://github.com/AlsheikhMedia/asm-skills/releases):

```bash
claude install ./<skill-name>.skill
```

## What Are Claude Code Skills?

Skills are markdown instruction sets that extend what Claude Code can do. When you install a skill, Claude Code loads it automatically when context matches — no slash commands needed. Each skill contains expert-level checklists, frameworks, and decision trees that Claude follows to produce structured, actionable output.

Skills live in your project's `.claude/skills/` directory. They're just files — you can read, edit, and version them like any other code.

## Contributing

PRs welcome. Each skill lives in `skills/<skill-name>/` with a `SKILL.md` and optional `references/`, `scripts/`, `assets/` directories.

See the [skill format spec](https://code.claude.com/docs/en/skills) for structure requirements.

## License

MIT — see [LICENSE](LICENSE). Note: `cro-funnel` is adapted from [AgentKits Marketing](https://github.com/aitytech/agentkits-marketing) (MIT).
