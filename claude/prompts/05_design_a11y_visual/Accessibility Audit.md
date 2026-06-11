# Accessibility Audit

## Mode

- Use the active `CLAUDE.md` context if present, then repository evidence.
- Work in the current Claude Code Cloud session. Do not assume hidden background runs or extra delegation mechanisms unless the user explicitly provides them.
- Analysis-only mode: inspect the repository, do not edit product code.

## Goal

Audit reachable accessibility defects in critical user/admin/public paths. Keep only issues supported by repository evidence and observable behavior; do not produce generic WCAG checklists without an owner and affected surface.

## Inspect

Routes/pages, layouts, shared components, forms, modals/drawers/popovers, tables/lists, navigation, toasts/alerts/status regions, media/assets, CSS/theme/tokens, keyboard/focus helpers, i18n/copy, tests, Storybook/previews, accessibility tooling, and generated design docs.

## Issue classes

Look for concrete, reachable issues in:

- Semantics and structure: invalid heading order that hurts comprehension, clickable non-controls, landmark gaps, incorrect list/table/form semantics, and hidden content exposed incorrectly.
- Names and descriptions: missing/incorrect accessible names, vague links/buttons, icon-only controls, unlabeled fields, broken error associations, missing alt/fallback text where needed.
- Keyboard and focus: unreachable controls, focus traps, lost focus after async updates, bad tab order, missing escape/close behavior, disabled action ambiguity, and destructive confirmation traps.
- Status and state announcements: loading/success/error/progress/toast/validation changes that are not perceivable or are announced unsafely.
- Visual accessibility: contrast/token risks, focus indicators, reduced-motion support where existing tokens/patterns support fixes, zoom/overflow issues, and touch target failures.
- Regression resistance: no tests/stories/previews for a critical accessible interaction, stale docs, or shared components that make repeated a11y regressions likely.

## Priority model

### P0

Inaccessible critical path, destructive action risk, auth/payment/data/admin path blocked for keyboard/screen-reader users, or permission/plan state that can mislead users into unsafe action.

### P1

Important reachable accessibility gap on a main path, shared component defect likely to repeat, broken focus/status behavior, or missing accessible names/validation on high-use forms.

### P2

Lower-risk but concrete accessibility improvement: minor landmark/name drift, weak focus affordance, missing story/test for an important state, or non-critical responsive/zoom issue.

## Work item quality

- Output findings as compact chat work items; do not assume a platform-specific task workflow or extra delegation mechanism.
- Each work item must cite `path:line[-line]` evidence for the affected owner and reachable surface.
- Include affected user path, expected accessible behavior, acceptance criteria, and validation direction such as keyboard trace, accessibility test, preview, or screenshot.
- Merge issues by owner when one fix addresses multiple surfaces.
- Do not report purely theoretical standard violations without reachable product impact.

## Output contract

Produce chat work items grouped by P0/P1/P2. If none qualify, output each priority with `None`. Use compact chat bullets; do not force a rigid work-item schema.
