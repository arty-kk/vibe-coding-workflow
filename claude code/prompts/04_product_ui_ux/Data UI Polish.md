# Data UI Polish — Tables, Lists, Filters, Bulk Actions, and Exports

## Mode

- Use the active `CLAUDE.md` context if present, then repository evidence.
- Work in the current Claude Code Cloud session. Do not assume hidden background runs or extra delegation mechanisms unless the user explicitly provides them.
- Implementation mode: change the repository when a focused data-UI improvement is justified by current evidence.

## Goal

Improve one coherent data-browsing or data-management surface: table, list, dashboard, admin grid, filter/search panel, bulk action, export/import state, or detail drawer. The diff should make data easier to understand, act on, and recover from without changing domain rules unnecessarily.

## Scope selection

- If the user named a table/list/dashboard/filter/export/bulk-action issue, polish that surface and directly affected states.
- If the request is broad, inspect high-use data surfaces and choose the highest-confidence fix with task-completion, safety, or support impact.
- Include related copy, accessibility, pagination/sorting/filtering, tests, i18n, and analytics hooks when they belong to the same data-UI problem.
- Avoid backend query rewrites, schema changes, new table libraries, and visual redesigns unless required by the selected issue.

## Polish targets

- Data comprehension: titles, descriptions, column names, units, dates/numbers, badges/statuses, row density, truncation, tooltips, summaries, and detail affordances.
- Controls: search, filters, sorting, pagination, tabs, saved views, refresh, selection, bulk actions, row actions, export/import, and reset/clear behavior.
- States: loading/skeleton, empty, no-results, error, stale/refreshing, partial data, permission/plan/tenant restrictions, destructive/bulk confirmations, and success feedback.
- Responsive behavior: table-to-card fallback, horizontal overflow, sticky controls, mobile action placement, and touch target safety.
- Accessibility: table semantics, header associations, keyboard selection/action flow, status announcements, and visible focus.
- Directly affected tests, snapshots, docs, and localization catalogs when the repo uses them.

## Implementation principles

- Reuse existing table/list components, query state patterns, route params, API contracts, i18n, and formatting utilities.
- Align visible data states with actual fetching/cache/error behavior.
- Preserve sorting/filtering/export semantics unless the requested polish is a behavior correction.
- Keep dangerous and bulk actions explicit, reversible where possible, and permission-aware.

## Validation

Run relevant repository-native checks. When possible, trace at least one non-empty state, empty/no-results state, loading/error state, and action state. Use preview/screenshot tooling when available.

## Final response

Respond in Russian with compact emoji sections: ♻️ changed data surface, 📁 key files, 🔎 evidence anchors, 🧪 checks, 👀 manual data-UI trace, ⚠️ assumptions/risks, ⛔ not run/not included.
