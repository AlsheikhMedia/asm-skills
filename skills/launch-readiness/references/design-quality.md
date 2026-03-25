# Design Quality Checklist

## Design System {#design-system}

A design system ensures visual consistency across every page. Without one, each page looks like it was built by a different person (because it was — you at different times, in different moods).

### What to Check

- [ ] Color palette defined (primary, secondary, neutrals, semantic colors for success/warning/error/info)
- [ ] Colors documented with exact values (hex/HSL), not just "use teal"
- [ ] Accessible contrast ratios verified (4.5:1 minimum for text)
- [ ] Typography scale defined (font families, sizes, weights, line heights)
- [ ] Spacing scale defined (consistent increments: 4px, 8px, 12px, 16px, 24px, 32px, 48px, 64px)
- [ ] Border radius tokens defined (small, default, large)
- [ ] Shadow tokens defined (if shadows are used)
- [ ] Component library chosen and configured (shadcn, Radix, Headless UI, etc.)
- [ ] Dark mode considered (even if deferred — "not doing dark mode yet" is a decision, not an oversight)
- [ ] RTL support considered (if targeting RTL markets: logical CSS properties, not physical)
- [ ] Design tokens stored in code (CSS variables, Tailwind config, or theme file — not just in Figma)

### Minimum Viable Design System Document

If no design system exists, create one covering:

```markdown
# Design System

## Colors

- Primary: [hex] — used for CTAs, links, active states
- Secondary: [hex] — used for headers, emphasis
- Neutral: [scale from 50-900] — used for text, backgrounds, borders
- Success: [hex] | Warning: [hex] | Error: [hex] | Info: [hex]

## Typography

- Body: [font family], [base size], [line height]
- Headings: [font family], [weight]
- Code: [monospace font]
- Scale: xs(12) sm(14) base(16) lg(18) xl(20) 2xl(24) 3xl(30)

## Spacing

- Base unit: 4px
- Scale: 1(4) 2(8) 3(12) 4(16) 6(24) 8(32) 12(48) 16(64)

## Components

- Library: [shadcn / Radix / custom]
- Icon set: [Lucide / Heroicons / custom]
```

### Common Mistakes

- Using Tailwind's default colors instead of defining project-specific tokens (every page looks like a Tailwind template)
- Inconsistent spacing ("sometimes 16px, sometimes 15px, sometimes 20px")
- No semantic color tokens (hardcoding `text-red-500` instead of `text-destructive`)
- Physical CSS properties in RTL-target apps (`margin-left` instead of `margin-inline-start`)

---

## Page-Type Specifications {#page-specs}

Every page in a SaaS app falls into one of a few types. Defining specs per type means you don't reinvent patterns for every new page — you follow the type's checklist and know it'll be consistent.

### What to Check

- [ ] Page types identified (typically: List, Detail, Form/Dialog, Dashboard)
- [ ] Each type has a checklist of required elements (MUST have vs SHOULD have)
- [ ] Checklists cover: layout, data states, navigation, accessibility, responsive behavior
- [ ] New pages are built against their type's checklist (enforced, not optional)
- [ ] Existing pages audited against checklists (gaps documented)

### Standard Page Types for B2B SaaS

**List Page** — displays a table/grid of entities

```
Required elements:
- Page header (title, subtitle, action buttons)
- Stat cards (summary metrics above the table)
- Search (debounced, URL-driven)
- Filters (URL-driven, "clear all" button when active)
- Data table (sortable columns, responsive column hiding)
- Row actions (view, edit, delete with confirmation)
- Pagination (URL-driven, page size selector, "showing X of Y")
- Empty state (when no results or no data)
- Loading state (skeleton, not spinner)
- Row click → detail page navigation
```

**Detail Page** — displays a single entity

```
Required elements:
- Breadcrumb navigation (not just a back arrow)
- Header card (avatar/icon, name, status badges, action buttons)
- "More" dropdown (secondary actions: suspend, delete, etc.)
- Tabbed layout (Overview + Activity at minimum)
- Tab state in URL hash (deep-linkable)
- Info sections (labeled fields, 2-column grid)
- Related entities section (with counts and links)
- Activity/audit tab (timestamped log of changes)
- Data states (loading skeleton, error, 404)
- Contact touchpoints (email as mailto:, phone as tel:)
```

**Form / Dialog** — creates or edits an entity

```
Required elements:
- Form validation (client + server, Zod schemas)
- Error messages per field (not just a generic toast)
- Loading state on submit button (disable + spinner)
- Success feedback (toast + redirect or close)
- Unsaved changes guard (warn before navigating away)
- Keyboard support (Tab order, Enter to submit, Escape to cancel)
```

**Dashboard** — overview/summary page

```
Required elements:
- KPI cards (icon, label, value, change indicator)
- KPI click-through to filtered list
- Two-column layout (primary wider, secondary narrower)
- Section headers with "View all" links
- Time-aware greeting ("Good morning, [name]")
- Time range selector (Today / 7d / 30d)
- Loading skeleton per widget
- Empty/first-run state (onboarding CTA, not blank page)
- Role-specific content (different KPIs per role)
```

### Cross-Cutting Concerns (Apply to ALL pages)

These apply regardless of page type:

- `<head>` title set (not empty or default)
- Toast notifications on every mutation (success + error)
- No console errors during normal navigation
- Responsive at 375px (mobile), 768px (tablet), 1024px+ (desktop)
- No horizontal overflow on any viewport
- Dates in locale-appropriate format (not hardcoded US format)
- Timezone-aware (display in user's timezone or app's configured timezone)
- Logical CSS only if targeting RTL markets (ms-/me-/ps-/pe-, not ml-/mr-/pl-/pr-)

### How to Build Page-Type Specs

1. Identify every page in the app and classify it by type
2. For each type, list what's required (MUST) and what's nice-to-have (SHOULD)
3. Build shared components that implement the type's patterns (Breadcrumb, StatCards, ActivityTab, etc.)
4. Audit existing pages against the checklist
5. Fix systemic gaps first (missing across many pages), then per-page gaps

### Enforcement

Page-type specs are only useful if they're enforced. Three layers:

**Layer 1 — CLAUDE.md rule**: Tell Claude Code to check the page-type spec before declaring any page complete.

**Layer 2 — E2E tests**: Write Playwright tests that verify page-type requirements (breadcrumbs visible, tabs sync with hash, etc.).

**Layer 3 — Manual audit**: Periodically run a full audit of all pages against the spec. Track compliance score over time.
