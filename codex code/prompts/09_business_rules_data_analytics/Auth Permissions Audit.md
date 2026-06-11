# Auth Permissions Audit

## Mode

- Use the active `AGENTS.md` chain.
- Plan mode only: inspect the repository, do not edit product code.

## Goal

Audit authentication, authorization, tenancy, roles, session boundaries, and permission-gated UI/API behavior. Keep only reachable issues that can cause unauthorized access, user confusion, broken legitimate access, or maintainability drift in permission logic.

## Inspect

Auth middleware/guards, session/JWT/cookie handling, route protection, server actions/API handlers, role/permission models, tenant/workspace/project scoping, plan/entitlement gates, admin impersonation, invitation/member flows, frontend route guards, disabled/hidden UI actions, audit logs, tests, seed data, migrations, docs, and generated maps when present.

## Issue classes

Look for concrete, reachable issues in:

- Boundary gaps: protected data or mutations reachable without the expected session, role, tenant, ownership, plan, or feature gate.
- Scope confusion: user/workspace/project/org IDs accepted from the client without owner-layer verification, inconsistent tenant filters, unsafe cache keys, or cross-tenant search/index leakage.
- Role drift: duplicated permission checks, UI-only enforcement, inconsistent admin/member semantics, stale enum values, or migrations that do not match application checks.
- Session lifecycle: weak logout/session invalidation, invitation/recovery token handling, refresh behavior, impersonation escape, missing CSRF protection where relevant, or unsafe redirect handling.
- UX/API mismatch: UI hides/shows actions incorrectly, backend rejects valid actions without recovery, forbidden states have misleading copy, or plan gates conflict with entitlements.
- Regression resistance: missing tests for role boundaries, tenant isolation, forbidden mutations, invitation flows, ownership transfer, and no-access UI states.

## Priority model

### P0

Unauthorized data exposure, unauthorized destructive/paid/admin mutation, cross-tenant access, privilege escalation, or token/session flaw on a reachable path.

### P1

Broken legitimate access on an important path, duplicated permission logic likely to drift, missing critical permission tests, unsafe tenant scoping pattern, or misleading UI/API auth behavior with meaningful impact.

### P2

Lower-risk permission maintainability issue, weak no-access copy, stale auth docs, minor inconsistent role naming, or test/docs gap that does not currently expose a critical path.

## Output contract

Create focused task-subs only for concrete repo-supported findings. Each finding must include evidence anchors as `path:line[-line]`, owner boundary, affected roles/scopes, impact, and validation path. Do not include generic security advice without repository evidence.
