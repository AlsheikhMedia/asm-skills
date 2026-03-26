# Design/UX — Impact Checklist

When a feature, task, or initiative affects the Design/UX team, use this checklist to identify specific deliverables, dependencies, and risks.

## What to Check

### UI Changes
- [ ] New pages or views needed
- [ ] Existing components modified (layout, behavior, states)
- [ ] New shared components required (reusable across features)
- [ ] Design system updates (new tokens, component variants, patterns)
- [ ] Icon or illustration needs
- [ ] Empty states, loading states, error states designed
- [ ] Responsive behavior specified (mobile, tablet, desktop breakpoints)

### Prototyping & Validation
- [ ] Wireframes or mockups needed before development starts
- [ ] Interactive prototype needed (for complex interactions)
- [ ] User flow diagrams needed (for multi-step processes)
- [ ] Usability concerns identified and addressed

### Accessibility
- [ ] Color contrast meets WCAG 4.5:1 minimum
- [ ] Touch targets meet 48px minimum (56px for primary CTAs)
- [ ] Keyboard navigation path defined
- [ ] Screen reader labels specified
- [ ] RTL support considered (if targeting RTL markets — logical CSS only)
- [ ] Reduced motion alternatives provided (for animations)

### Design System Impact
- [ ] New tokens needed (colors, spacing, typography)
- [ ] Existing component variants sufficient or new ones needed
- [ ] Pattern documentation updated
- [ ] Design-to-dev handoff documented (specs, assets, annotations)

## Typical Dependencies

**Design/UX needs FROM:**

| Department | What | Why |
|-----------|------|-----|
| Product | Requirements, user flows, feature scope, content | Can't design without knowing what to design |
| Research | User insights, pain points, behavioral data | Design decisions need user context |
| Brand | Visual identity guidelines, tone of voice | Must stay on-brand |
| Development | Technical constraints, feasibility feedback | Can't design what can't be built |

**Design/UX PRODUCES for:**

| Department | What | Why |
|-----------|------|-----|
| Development | Mockups, component specs, interaction patterns, assets | Dev needs visual specs to implement |
| Product | Feasibility feedback, UX recommendations, flow improvements | Product needs design input on specs |
| Marketing/Content | Visual assets, brand-consistent templates | Marketing needs on-brand creative |
| QA/Testing | Visual reference for acceptance testing | QA needs to know what "correct" looks like |

## Common Deliverables by Initiative Type

### New Feature
- [ ] Wireframes (low-fidelity for review)
- [ ] Mockups (high-fidelity for development)
- [ ] Component specs (spacing, colors, typography, states)
- [ ] Interaction specs (hover, focus, active, disabled, loading)
- [ ] Responsive breakpoint behavior
- [ ] Asset exports (icons, illustrations)

### Feature Enhancement
- [ ] Updated mockups showing changes
- [ ] Component state additions (if new states needed)
- [ ] Before/after comparison for review

### Design System Update
- [ ] New token definitions
- [ ] Component documentation
- [ ] Migration guide (if changing existing patterns)

## Effort Estimation Guide

| Deliverable | Typical Range |
|------------|--------------|
| Wireframe (single page) | 0.5-1 day |
| High-fidelity mockup (single page) | 1-2 days |
| Component spec (new component) | 0.5-1 day |
| Interactive prototype | 1-3 days |
| Full feature design (multi-page) | 3-7 days |
| Design system update | 1-3 days |
| Icon/illustration set | 1-2 days |

## Common Mistakes

- Starting development before design review (rework when specs change)
- Designing only the happy path (missing empty states, errors, edge cases)
- Skipping mobile/responsive design (discovered late, costs more to fix)
- Not specifying interaction states (hover, focus, disabled, loading)
- No design-dev handoff documentation (developers interpret ambiguously)
- Ignoring accessibility until QA flags it (retrofit is expensive)
- Designing in isolation without technical feasibility check
