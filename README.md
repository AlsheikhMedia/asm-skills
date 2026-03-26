# ASM Skills

Production-grade skills for Claude Code by [AlSheikh Media](https://alsheikhmedia.com).

Born from shipping real SaaS products — not theory. Each skill encodes the checklists, patterns, and strategies we use in production.

## Skills

### Infrastructure

| Skill | What it does |
| --- | --- |
| [launch-readiness](skills/launch-readiness/) | 12-domain SaaS audit: error monitoring, CI/CD, migrations, staging, design system, page specs, unit tests, E2E tests, seed data, security, observability, feature flags. Works for new projects (bootstrap) and existing ones (audit gaps). |
| [save](skills/save/) | End-of-session progress saver. Updates memory, commits changes, and handles push confirmation. |

### Workflow

| Skill | What it does |
| --- | --- |
| [chain](skills/chain/) | Run predefined workflow chains — multi-step sequences that execute skills in order with optional pause points for review. |
| [chain-create](skills/chain-create/) | Create or edit workflow chains. Saves chain definitions to `.claude/chains.json`. |

### Marketing

| Skill | What it does |
| --- | --- |
| [copywriting](skills/copywriting/) | Write, rewrite, or improve marketing copy for any page — homepage, landing, pricing, feature, about. |
| [marketing-ideas](skills/marketing-ideas/) | 139 proven marketing strategies organized by category. Match ideas to your stage, resources, and goals. |
| [marketing-psychology](skills/marketing-psychology/) | 70+ mental models for marketing — cognitive bias, persuasion, behavioral science applied to conversion. |
| [product-marketing-context](skills/product-marketing-context/) | Create a reusable product marketing context doc (`.claude/product-marketing-context.md`) that other marketing skills reference. |
| [programmatic-seo](skills/programmatic-seo/) | Build SEO-driven pages at scale using templates and data — directory pages, comparison pages, location pages. |
| [seo-audit](skills/seo-audit/) | Diagnose SEO issues: on-page, technical SEO, meta tags, structured data, content quality. |

### CRO (Conversion Rate Optimization)

| Skill | What it does |
| --- | --- |
| [cro-funnel](skills/cro-funnel/) | Full-funnel CRO for SaaS: page optimization, form design, signup flow, onboarding activation, popup/modal design, paywall/upgrade screens. |
| [page-cro](skills/page-cro/) | Single-page conversion optimization for marketing pages — homepage, landing, pricing, feature, or blog. |

### Operations

| Skill | What it does |
| --- | --- |
| [feature-impact](skills/feature-impact/) | Cross-departmental impact analysis for features and initiatives. Maps which departments are affected, what each needs to deliver, dependency chains, risks, and execution order with parallel tracks. Adapts to any org structure. |

## Install

### Claude Code (recommended)

```bash
claude install github:AlsheikhMedia/asm-skills/skills/<skill-name>
```

For example:

```bash
claude install github:AlsheikhMedia/asm-skills/skills/launch-readiness
claude install github:AlsheikhMedia/asm-skills/skills/copywriting
claude install github:AlsheikhMedia/asm-skills/skills/cro-funnel
```

### Manual

Copy the skill folder into your project's `.claude/skills/` directory:

```bash
git clone https://github.com/AlsheikhMedia/asm-skills.git
cp -r asm-skills/skills/<skill-name> .claude/skills/
```

### From .skill file

Download the `.skill` file from [Releases](https://github.com/AlsheikhMedia/asm-skills/releases) and install:

```bash
claude install ./<skill-name>.skill
```

## Contributing

PRs welcome. Each skill lives in `skills/<skill-name>/` with a `SKILL.md` and optional `references/`, `scripts/`, `assets/` directories.

See the [skill format spec](https://code.claude.com/docs/en/skills) for structure requirements.

## License

MIT
