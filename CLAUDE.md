# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

A collection of Claude Code skills by AlSheikh Media for solo founders and small teams. Skills are markdown-based instruction sets that Claude Code loads on demand to perform domain-specific tasks (audits, bootstrapping, etc.).

## Repository Structure

```
skills/<skill-name>/
  SKILL.md              # Main skill file — frontmatter (name, description) + instructions
  references/           # Supporting docs loaded lazily during skill execution
  scripts/              # Optional automation scripts
  assets/               # Optional static assets
dist/                   # Packaged .skill files (gitignored, built by CI)
```

Each skill is self-contained in its directory. `SKILL.md` is the entry point — its YAML frontmatter `description` field controls when Claude Code triggers the skill.

## Packaging & Releases

Skills are packaged into `.skill` files (zip archives) by the GitHub Actions workflow in `.github/workflows/package-skills.yaml`:

- **On release creation**: packages all skills, uploads `.skill` files as release assets
- **On workflow_dispatch**: packages all skills, uploads as build artifacts

Packaging command (what CI runs per skill):
```bash
cd skills/<skill-name> && zip -r ../../dist/<skill-name>.skill . -x "*.DS_Store" "__pycache__/*" "node_modules/*" "evals/*"
```

## Adding a New Skill

1. Create `skills/<skill-name>/SKILL.md` with proper frontmatter (`name`, `description`)
2. Add `references/`, `scripts/`, `assets/` directories as needed
3. Update the skill table in `README.md`
4. Create a GitHub release — CI auto-packages all skills

## Installation Methods

```bash
# Via Claude Code CLI (recommended)
claude install github:AlsheikhMedia/asm-skills/skills/<skill-name>

# From .skill file
claude install ./dist/<skill-name>.skill
```

## Current Skills (13)

### Infrastructure
- **launch-readiness**: 12-domain SaaS audit (error monitoring, CI/CD, migrations, staging, design system, page specs, testing, E2E, seed data, security, observability, feature flags). Audit or bootstrap mode. Reference docs loaded lazily by domain tier.
- **save**: End-of-session progress saver — memory updates, commits, push confirmation.

### Workflow
- **chain**: Run predefined workflow chains from `.claude/chains.json`. Multi-step skill sequences with pause points.
- **chain-create**: Create/edit workflow chains.

### Marketing
- **copywriting**: Marketing copy for any page type. References `copy-frameworks.md` and `natural-transitions.md`.
- **marketing-ideas**: 139 categorized marketing strategies. References `ideas-by-category.md`.
- **marketing-psychology**: 70+ mental models for marketing application.
- **product-marketing-context**: Creates `.claude/product-marketing-context.md` referenced by other marketing skills.
- **programmatic-seo**: SEO-driven pages at scale. References `playbooks.md`.
- **seo-audit**: Technical + on-page SEO diagnosis. References `aeo-geo-patterns.md` and `ai-writing-detection.md`.

### CRO
- **cro-funnel**: Full-funnel CRO — forms, signup, onboarding, paywall. MIT license (AgentKits attribution).
- **page-cro**: Single-page conversion optimization. References `experiments.md`.

### Operations
- **impact**: Cross-departmental impact analysis + execution. 6-core department model (Product, Engineering, Design, QA, Marketing, Ops). Extended 14-department mode via `.claude/org-structure.md`. Tracks deliverables via GitHub/GitLab/Codeberg/Bitbucket/local. 7 built-in execution modules: tech-writer, legal, social-media, analyst, support, finance, brand. v2.0.
