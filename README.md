# ASM Skills

Production-grade skills for Claude Code by [AlSheikh Media](https://alsheikhmedia.com).

Born from shipping real SaaS products — not theory. Each skill encodes the checklists, patterns, and infrastructure requirements we use in production.

## Skills

| Skill                                        | What it does                                                                                                                                                                                                                                |
| -------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [launch-readiness](skills/launch-readiness/) | 12-domain SaaS audit: error monitoring, CI/CD, migrations, staging, design system, page specs, unit tests, E2E tests, seed data, security, observability, feature flags. Works for new projects (bootstrap) and existing ones (audit gaps). |

More skills coming soon.

## Install

### Claude Code (recommended)

```bash
claude install github:AlsheikhMedia/asm-skills/skills/launch-readiness
```

### Manual

Copy the skill folder into your project's `.claude/skills/` directory:

```bash
git clone https://github.com/AlsheikhMedia/asm-skills.git
cp -r asm-skills/skills/launch-readiness .claude/skills/
```

### From .skill file

Download the `.skill` file from [Releases](https://github.com/AlsheikhMedia/asm-skills/releases) and install:

```bash
claude install ./launch-readiness.skill
```

## Usage

Once installed, trigger the skill by asking Claude Code:

- "Audit my project for launch readiness"
- "Am I ready to launch?"
- "What infrastructure am I missing?"
- "Set up CI/CD, error monitoring, and staging"
- "Pre-launch checklist"
- "Bootstrap a new SaaS project"

The skill operates in two modes:

**Audit mode** — scans an existing codebase against 12 domains, produces a gap report with prioritized fixes and time estimates.

**Bootstrap mode** — walks through each domain for a new project, generates config, code, and docs to set everything up.

## What launch-readiness covers

### Tier 1 — Blocks everything else

1. Error Monitoring (Sentry/equivalent — SDK, source maps, alerts)
2. CI/CD Pipeline (lint, test, build chain with PR gates)
3. Database Migrations (versioned, scripted, no raw SQL in prod)
4. Staging Environment (separate env, deploy-before-prod workflow)

### Tier 2 — Before first customer

5. Design System (tokens, typography, spacing, color palette)
6. Page-Type Specs (list, detail, form, dashboard checklists)
7. Unit & Integration Tests (critical paths, ORM, API tests)
8. E2E Tests (happy path journeys, auth setup, responsive)
9. Seed Data & Demo Environment (idempotent, realistic data)
10. Security Baseline (headers, rate limiting, CORS, auth guards)

### Tier 3 — Professional grade

11. Observability (analytics, performance budgets, uptime, logging)
12. Feature Flags (toggle system, per-org overrides, admin UI)

## Framework support

Adapts recommendations to your stack. Framework-specific guidance included for:

- **SvelteKit** (hooks, +page.server.ts loaders, svelte.config.js)
- **Next.js** (middleware.ts, API routes, server components)
- **Nuxt** (server middleware, composables, Nitro)
- **General** (applies to any web framework)

## Contributing

PRs welcome. Each skill lives in `skills/<skill-name>/` with a `SKILL.md` and optional `references/`, `scripts/`, `assets/` directories.

See the [skill format spec](https://code.claude.com/docs/en/skills) for structure requirements.

## License

MIT
