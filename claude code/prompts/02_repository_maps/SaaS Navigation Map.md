# SaaS Navigation Map

## Mode

- Use the active `CLAUDE.md` context if present, then repository evidence.
- Work in the current Claude Code Cloud session. Do not assume hidden background runs or extra delegation mechanisms unless the user explicitly provides them.
- Analysis/documentation mode: create or update a repository map, not product behavior.

## Goal

Create or update `docs/nav_map.md` as a current map of SaaS routes, layouts, modals/drawers, forms, tables, navigation, roles, plans, tenants, and key UI states.

## Inspect

Routing, layouts, pages, guards, loaders/actions, API hooks, state stores, forms, tables, dialogs, navigation components, auth/RBAC, plan/billing/quota code, tenant/workspace/project context, i18n, analytics/observability, tests, docs, and generated route maps.

## Map content

### Evidence and IDs

- Write or update `docs/nav_map.md` when the environment allows it. If writing is unavailable, print the complete markdown content in chat.
- Use stable IDs and preserve existing IDs when refreshing: route `R-*`, layout `L-*`, modal/drawer `M-*`, form `F-*`, table/list `T-*`, guard `G-*`.
- Anchor every entry to current repository evidence with `path:line[-line]` plus symbol when possible.
- Distinguish source-of-truth implementation from generated docs, generated clients, stale docs, and inferred behavior.
- Capture unknowns only when they affect future audit or implementation.

### Coverage

Capture product context when discoverable: app type, primary roles, tenant model, plan model, auth/onboarding model, main entity graph. Cover user, admin/staff, public/auth, no-access/no-plan/over-quota, empty/loading/error, destructive, and async states when present.

### Entry details

For each route/surface, capture path or trigger, owner symbol, layout, roles/guards, plan/tenant behavior, data dependencies, actions, states, forms/tables/modals involved, tests, and gaps.

## Markdown structure

Use a readable markdown hierarchy with summary first, then route tree, auth/onboarding entry points, layouts, routes, modals/drawers, forms, tables/lists, navigation surfaces, role/action/plan matrices, cross-cutting behavior, reachability, unknowns, and assumptions. Omit sections that do not exist in the repo. Do not invent surfaces, states, commands, endpoints, or contracts.

## Final response

Respond in Russian with compact status sections: ✅ map created/updated, 📁 file, 🔎 strongest evidence anchors, 🧪 checks/spot-checks, ⚠️ assumptions/unknowns.
