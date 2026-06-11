# Billing Entitlements Audit

## Mode

- Use the active `CLAUDE.md` context if present, then repository evidence.
- Work in the current Claude Code Cloud session. Do not assume hidden background runs or extra delegation mechanisms unless the user explicitly provides them.
- Analysis-only mode: inspect the repository, do not edit product code.

## Goal

Audit billing, plan, quota, entitlement, tenant, and permission behavior for correctness and user-visible consistency. Keep only issues with repository evidence; do not invent pricing rules, plan names, provider behavior, or business policy.

## Inspect

Plan definitions, billing provider integration, webhook handlers, subscription state, entitlement/feature-flag helpers, quota counters, RBAC/tenant/workspace ownership, route/API guards, UI gates, upgrade/downgrade/trial/cancel flows, invoices/payment states, jobs/reconciliation, tests, docs, and env/config.

## Issue classes

Look for concrete, reachable issues in:

- Source-of-truth drift: different plan/quota/feature rules across UI, API, workers, docs, tests, and provider mapping.
- Enforcement gaps: visible actions not server-enforced, disabled UI hiding allowed operations, missing tenant/role checks, stale subscription state, or quota race conditions.
- Lifecycle bugs: trial start/end, upgrade/downgrade, cancel/reactivate, payment failure, grace period, webhook retry/order/idempotency, and reconciliation gaps.
- User-facing clarity: no-access/no-plan/over-quota/upgrade copy contradicts actual entitlements or provides unsafe diagnostics.
- Data safety: cross-tenant billing exposure, wrong invoice/account owner, destructive plan action without confirmation/audit trail.
- Regression resistance: missing tests for plan matrix, webhook idempotency, quota boundaries, or UI/API gate alignment.

## Priority model

### P0

User can access paid/forbidden data/actions, loses paid access incorrectly, cross-tenant billing/data leak, unsafe webhook mutation, or destructive billing state corruption.

### P1

Important entitlement drift, quota/plan race, misleading upgrade/no-access state, missing lifecycle handling, or missing tests for high-value billing paths.

### P2

Lower-risk but concrete billing quality issue: stale docs, copy mismatch, minor plan matrix inconsistency, secondary lifecycle gap, or weak regression coverage.

## Work item quality

- Output findings as compact chat work items; do not assume a platform-specific task workflow or extra delegation mechanism.
- Each work item must cite `path:line[-line]` evidence for entitlement source of truth and at least one consuming surface.
- Include affected plan/role/tenant state, expected behavior, acceptance criteria, and validation direction.
- Merge issues by entitlement owner when one fix validates them together.

## Output contract

Produce chat work items grouped by P0/P1/P2. If none qualify, output each priority with `None`. Use compact chat bullets; do not force a rigid work-item schema.
