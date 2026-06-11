# UI Surface Audit

## Mode

- Use the active `AGENTS.md` chain.
- Plan mode only: inspect the repository, do not edit product code.

## Goal

Audit concrete UI surfaces for visual hierarchy, component-system consistency, responsive behavior, accessibility, state completeness, and implementation drift. This produces task-subs; use `Web Polish.md`, `SaaS Polish.md`, or `UX Flow Polish.md` for execution.

## Inspect

Routes/pages, layouts, components, design tokens, theme/config files, CSS/Tailwind/styled-system usage, icons/assets, Storybook or design docs, forms/tables/modals, state components, i18n/copy, accessibility helpers, tests/snapshots, screenshots/preview tooling, generated maps/docs, and analytics hooks where present.

## Issue classes

Look for concrete, reachable issues in:

- Hierarchy and layout: unclear page structure, broken responsive behavior, overflow/clipping, inconsistent spacing/typography, and action placement that hurts task completion.
- Component-system drift: ad-hoc styles, duplicated variants, mixed tokens, inconsistent interaction states, and forked components that can diverge.
- State completeness: missing loading/empty/error/disabled/no-access/no-plan/over-quota/destructive/pending/partial-success states on reachable surfaces.
- Accessibility: missing accessible names, semantic structure issues, focus traps, keyboard gaps, status announcements, contrast/reduced-motion problems where repo tokens support fixes.
- Forms/tables/data UI: unclear labels, validation messages, sorting/filtering affordances, pagination state, bulk/destructive action safety, and recovery paths.
- Implementation drift: UI promises not backed by API/state, stale docs/design maps, fragile snapshots, or tests that miss observable UI behavior.

## Priority model

### P0

Reachable UI issue causing destructive mistake, permission/plan confusion with data/security impact, inaccessible critical path, or UI/API contradiction that breaks a core workflow.

### P1

Important flow friction, missing critical state, component drift likely to regress, accessibility gap on a main path, or misleading user-facing behavior with meaningful impact.

### P2

Lower-risk but concrete UI quality issue: minor responsive bug, inconsistent token/variant, weak empty/error copy, stale design docs, or maintainability coupling that blocks safe UI change.

## Task-sub quality

- Use native Codex Cloud task-sub creation when available; do not force a handmade markdown task-sub body.
- Every task-sub must cite `path:line[-line]` evidence for the surface/component owner and affected route/state, plus symbol when possible.
- Include affected user role/state, expected UI behavior, acceptance criteria, and validation direction including preview/screenshot when available.
- Use one unambiguous fix direction per task-sub; no alternatives.
- Merge symptoms under the same UI owner/source of truth unless fixes, rollout units, or validation differ.
- Do not report taste-only visual preferences without comprehension, accessibility, conversion, permission, or task-completion impact.

## Output contract

Produce only native Codex Cloud task-subs grouped by P0/P1/P2. If none qualify, output each priority with `None`. Do not print a custom task-sub schema.
