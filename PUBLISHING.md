# Publishing Guide — ASM Skills

## 1. GitHub (AlsheikhMedia/asm-skills)

```bash
# From the asm-skills/ directory
cd asm-skills
git init
git add .
git commit -m "Initial release: launch-readiness skill

12-domain SaaS launch readiness audit covering error monitoring,
CI/CD, migrations, staging, design system, page specs, testing,
seed data, security, observability, and feature flags."

# Create the repo on GitHub (public)
gh repo create AlsheikhMedia/asm-skills --public --source=. --push

# Create first release (triggers .skill packaging via GitHub Actions)
gh release create v1.0.0 \
  --title "v1.0.0 — launch-readiness" \
  --notes "First release. Includes the launch-readiness skill for SaaS project auditing and bootstrapping." \
  dist/launch-readiness.skill
```

After this, the skill is installable via:
```bash
claude install github:AlsheikhMedia/asm-skills/skills/launch-readiness
```

## 2. skills.sh

skills.sh indexes public GitHub repos automatically. Once the repo is public on GitHub:

1. Go to https://skills.sh
2. Search for your repo or submit it manually
3. The skill becomes discoverable at: `skills.sh/AlsheikhMedia/asm-skills`

Users install via:
```bash
npx skills add AlsheikhMedia/asm-skills/skills/launch-readiness
```

If skills.sh requires explicit submission, check their docs for a submit form or CLI command.

## 3. Claude Code Plugin Marketplace

The official Anthropic marketplace requires a review process:

1. Go to https://github.com/anthropics/claude-plugins-official
2. Follow their submission guidelines (typically a PR or form)
3. Include the `.skill` file from `dist/launch-readiness.skill`
4. Provide: skill name, description, author, license, and a link to the GitHub repo

Alternative — direct `.skill` install (no marketplace needed):
```bash
claude install ./dist/launch-readiness.skill
```

## Adding New Skills

When adding a new skill to the collection:

1. Create `skills/<skill-name>/SKILL.md` with proper frontmatter
2. Add optional `references/`, `scripts/`, `assets/` directories
3. Update `README.md` skill table
4. Create a new release — GitHub Actions will auto-package all skills
5. Each skill gets its own `.skill` file in the release assets
