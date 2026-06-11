# SaaS Polish — Flows, Navigation, Copy, Permissions, and States

## Mode

- Use the active `AGENTS.md` chain.
- Execute mode: change the repository when changes are justified by current evidence.

## Goal

Improve a coherent SaaS product surface or journey across UX, copy, permissions, plan/tenant behavior, navigation, states, and accessibility. Produce a complete reviewable batch for the selected surface rather than a tiny isolated edit when adjacent states are part of the same problem.

## Scope selection

- If the user named a flow, route, role, plan, component, or issue, polish that area and directly affected states.
- If the request is broad, inspect primary authenticated/public SaaS surfaces and apply the highest-confidence improvements with visible user impact.
- Include related RBAC, plan, tenant, copy, state, and accessibility fixes when they belong to the same journey.
- Avoid unrelated feature additions, pricing/business logic changes, visual redesigns, dependency changes, and backend rewrites unless the surface fix requires them.

## SaaS-specific targets

- Navigation, breadcrumbs, tabs, layout hierarchy, route guards, onboarding, settings, and recovery paths.
- RBAC/permissions: visible actions match allowed actions; disabled/no-access states explain the next step safely.
- Plan/quota/billing/trial gates: locked/upgrade/over-quota states are clear, consistent, and aligned with actual entitlements.
- Tenant/workspace/project context: switchers, names, ownership, persisted context, URLs, and cross-tenant copy are unambiguous.
- Forms, tables, filters, sorting, pagination, bulk actions, destructive actions, confirmations, and async operations.
- Empty/loading/error/disabled/no-permission/no-plan states and user-safe diagnostics.
- Terminology consistency, i18n catalogs, analytics/observability hooks where existing patterns require them.

## Implementation principles

- Reuse existing components, tokens, layout, validation, permission, plan-gate, data-loading, and i18n patterns.
- Fix the owner surface rather than scattering one-off text changes.
- Preserve current contracts unless the requested polish requires a behavior correction.
- Update directly affected tests, snapshots, docs, and localization catalogs when the repo uses them.

## Validation

Run relevant repository-native checks. When explaining non-obvious repo facts, skipped adjacent work, or detected behavior, cite `path:line[-line]` where useful.

For permission/plan changes, trace at least one allowed and one restricted state when possible.

## Final response

Respond in Russian with compact emoji sections: ♻️ changed surfaces, 📁 key files, 🧪 checks, 👀 manual review/trace, ⚠️ assumptions/risks, ⛔ not run/not included.
