# Web Polish — UX, Copy, Navigation, States, and Accessibility

## Mode

- Use the active `AGENTS.md` chain.
- Execute mode: change the repository when changes are justified by current evidence.

## Goal

Improve a coherent web UI surface across UX flow, copy, navigation, forms, states, and accessibility. The diff should make the selected surface feel complete, not merely tweak one token while adjacent broken states remain.

## Scope selection

- If the user named a page, component, flow, route, or issue, polish that surface and directly affected states.
- If the request is broad, inspect primary reachable surfaces and apply the highest-confidence improvements with visible user impact.
- Include related copy/state/a11y fixes when they belong to the same surface or user journey.
- Avoid unrelated features, visual redesigns, dependency changes, and backend behavior changes unless the UI fix requires them.

## Polish targets

- Page hierarchy, section headings, labels, CTAs, links, breadcrumbs, tabs, table/list affordances, and recovery paths.
- Forms: field labels, helper text, validation messages, submit states, destructive confirmations, and input constraints.
- Modals, drawers, popovers, toasts, alerts, banners, async/pending state, optimistic update feedback, and partial-success handling.
- Empty/loading/error/disabled/no-access/unavailable states and user-safe diagnostics.
- Accessibility: semantic structure, focus behavior, keyboard reachability, accessible names, status announcements, reduced-motion/contrast where existing tokens support it.
- Terminology consistency, i18n usage, and analytics/observability hooks where existing patterns require them.

## Implementation principles

- Reuse existing components, tokens, layout patterns, validation patterns, route conventions, and i18n architecture.
- Prefer source-of-truth copy/components over repeated literals.
- Keep claims truthful and backed by existing product behavior.
- Update directly affected tests, snapshots, docs, and localization catalogs when the repo uses them.

## Validation

Run relevant repository-native checks. When explaining non-obvious repo facts, skipped adjacent work, or detected behavior, cite `path:line[-line]` where useful.

For UI changes, use preview/screenshot tooling when available; otherwise state the limitation.

## Final response

Respond in Russian with compact emoji sections: ♻️ changed surfaces, 📁 key files, 🧪 checks, 👀 manual review/trace, ⚠️ assumptions/risks, ⛔ not run/not included.
