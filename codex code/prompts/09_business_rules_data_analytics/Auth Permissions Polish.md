# Auth Permissions Polish — Roles, Tenancy, Gates, and No-access States

## Mode

- Use the active `AGENTS.md` chain.
- Execute mode: change the repository when a focused auth/permission improvement is justified by current evidence.

## Goal

Fix one coherent authentication, authorization, tenancy, or permission-gated experience end to end. The patch should align owner-layer checks, API behavior, UI affordances, copy, and tests.

## Scope selection

- If the user named a role, route, endpoint, workspace, plan state, invitation flow, or access bug, polish that boundary and directly affected surfaces.
- If the request is broad, inspect permission seams and apply the highest-confidence improvement with security, correctness, or user-impact value.
- Include related no-access UI, error/copy, redirects, audit logging, and tests when they belong to the same access contract.
- Avoid broad auth rewrites, provider migrations, role-model redesigns, or entitlement changes unless required by the selected fix.

## Polish targets

- Server-side owner checks for role, tenant/workspace/project ownership, membership, plan/entitlement, invitation token, and admin/impersonation context.
- API/server action behavior: safe status codes, machine-readable errors, no data leakage in forbidden/not-found paths, and stable redirect/recovery behavior.
- UI behavior: hidden vs disabled actions, explanatory no-access/upgrade states, safe destructive states, and consistency between visible affordances and allowed operations.
- Shared permission helpers/types/tests to reduce drift across routes, handlers, components, workers, and generated clients.
- Session lifecycle, cache keys, query filters, and background/job/webhook contexts where they touch the same access boundary.

## Implementation principles

- Enforce permissions in the backend/owner layer, not only in UI.
- Preserve least privilege and existing public contracts unless the task authorizes a contract change.
- Reuse existing auth, membership, entitlement, route-guard, and test patterns.
- Avoid leaking whether protected resources exist unless the repo already defines that behavior safely.
- Update directly affected tests, fixtures, docs, generated types, and localization catalogs when the repo uses them.

## Validation

Run repository-native checks for allowed, forbidden, unauthenticated, wrong-tenant/wrong-owner, and relevant plan/role states. If a state cannot be exercised because fixtures/credentials are unavailable, state the limitation and the exact manual verification path.

## Final response

Respond in Russian with compact emoji sections: ♻️ changed access boundary, 📁 key files, 🔎 evidence anchors, 🧪 checks, 👀 role/state trace, ⚠️ assumptions/risks, ⛔ not run/not included.
