# SaaS Audit

## Mode

- Use the active `AGENTS.md` chain.
- Plan mode only: inspect the repository, do not edit product code.

## Goal

Audit SaaS product behavior, UX, permissions, plan/tenant logic, and operational states. Keep issues that affect real users, admins, billing/plan behavior, data consistency, or regression risk.

## Inspect

Routes, layouts, pages, forms, tables, modals/drawers, loaders/actions, API hooks, stores, auth/RBAC, plan/billing/quota code, tenant/workspace/project context, onboarding, settings, destructive flows, async jobs, i18n, analytics/observability hooks, tests, docs, and generated navigation maps.

## Issue classes

Look for concrete, reachable issues in:

- Authenticated and public journeys: onboarding, dashboard, CRUD flows, settings, admin/staff paths, invite/member flows, recovery paths.
- RBAC/permissions: visible actions must match allowed actions; no-access states must be safe and useful; object-level access must be consistent.
- Plan/quota/billing/trial gates: locked/upgrade/over-quota states, checkout/subscription lifecycle, feature availability, entitlement drift.
- Tenant/workspace/project context: switchers, entity ownership, cross-tenant copy, stale context, URLs, persisted selections, and data isolation.
- Forms/tables/navigation: labels, validation, filters, sorting, pagination, bulk/destructive actions, breadcrumbs, tabs, route guards.
- Async/user-visible states: loading, empty, error, disabled, pending, optimistic update, partial success, retry, toast/alert behavior.
- Copy/i18n/observability: terminology consistency, localized strings, safe diagnostics, analytics hooks where existing patterns require them.
- Data/API/UI synchronization: UI promises, API contracts, DB state, generated docs/maps, and tests that drift from current behavior.

## Priority model

### P0

Tenant/data leakage, permission or plan bypass, destructive mutation flaw, billing/subscription inconsistency, broken critical path, data loss, or high-impact API/UI/DB contradiction.

### P1

Important workflow friction or incorrect state, inconsistent permissions/plan UX, duplicate product/domain logic, missing error handling, shallow critical coverage, or hot-path UX performance issue.

### P2

Lower-risk but concrete polish or maintainability issue: misleading copy, incomplete empty/error state, localized inconsistency, minor navigation ambiguity, or coupling that blocks safe product change.

## Task-sub quality

- Use native Codex Cloud task-sub creation when available; do not force a handmade markdown task-sub body.
- Every task-sub must cite `path:line[-line]` evidence for the problematic behavior/contract and the owner layer, plus symbol when possible.
- Include reachable surface, affected actors/consumers/states, expected behavior, acceptance criteria, and validation direction when discoverable.
- Use one unambiguous fix direction per task-sub; no alternatives.
- Merge symptoms under the same behavior owner/source of truth unless fixes, rollout units, or validation differ.
- Do not report theoretical risks, stylistic preferences, or generic best practices without current repo impact.
- Include affected role, plan, tenant context, and surface when relevant.
- Do not report cosmetic preferences unless they affect comprehension, conversion, accessibility, permissions, or task completion.
