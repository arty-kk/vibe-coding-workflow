# Design System Audit

## Mode

- Use the active `AGENTS.md` chain.
- Plan mode only: inspect the repository, do not edit product code.

## Goal

Audit the implementation design system: tokens, components, variants, styles, layout primitives, interaction states, documentation, and test/story coverage. Keep only repo-visible issues that make UI work slower, inconsistent, inaccessible, fragile, or visibly divergent.

## Inspect

Theme config, tokens, CSS/Tailwind/styled-system files, shared components, page-level variants, icons/assets, Storybook or component docs, `DESIGN.md`, screenshots/previews, tests/snapshots, forms/tables/modals, layout primitives, i18n/copy patterns, and generated UI artifacts.

## Issue classes

Look for concrete, reachable issues in:

- Token ownership: duplicated hardcoded values, mixed units, drift between theme/config/docs, missing semantic tokens for repeated UI decisions.
- Component variants: inconsistent sizes/states, forked implementations, duplicated patterns, missing disabled/loading/error/focus/destructive variants.
- Style architecture: ad-hoc CSS, one-off Tailwind/class soup where a component owner exists, conflicting responsive patterns, fragile specificity, and style leakage.
- Accessibility baked into system: shared components missing accessible names, focus handling, keyboard support, status announcements, contrast-friendly variants, or semantic defaults.
- Documentation and regression resistance: stale `DESIGN.md`, missing stories/examples for core variants, fragile snapshots, no visual/test coverage for shared components.
- Implementation drift: public surfaces bypass the system, docs promise unavailable variants, or owner components do not match actual route usage.

## Priority model

### P0

Shared component or token defect that can cause destructive user mistakes, inaccessible critical paths, permission/plan confusion, broken core route layout, or widespread UI/API contradiction.

### P1

Component-system drift or missing shared state likely to cause repeated regressions, important accessibility gaps, inconsistent variants on main flows, or maintainability issues blocking safe UI work.

### P2

Lower-risk but concrete system issue: stale docs, duplicated styling, weak variant naming, minor responsive inconsistency, missing story/example, or local drift that has a clear owner.

## Task-sub quality

- Use native Codex Cloud task-sub creation when available; do not force a handmade markdown task-sub body.
- Every task-sub must cite `path:line[-line]` evidence for the owner token/component and at least one affected usage.
- Include expected system behavior, affected surfaces, acceptance criteria, and validation direction including preview/story/screenshot when available.
- Merge symptoms under one owner when they share source of truth and validation.
- Do not report taste-only preferences without system consistency, accessibility, maintainability, or user-impact evidence.

## Output contract

Produce only native Codex Cloud task-subs grouped by P0/P1/P2. If none qualify, output each priority with `None`. Do not print a custom task-sub schema.
