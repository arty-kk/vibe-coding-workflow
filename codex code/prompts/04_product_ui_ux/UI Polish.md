# UI Polish — Visual System, Responsive Behavior, and Interaction States

## Mode

- Use the active `AGENTS.md` chain.
- Execute mode: change the repository when a focused UI improvement is justified by current evidence.

## Goal

Improve one coherent visual UI surface at the implementation layer: hierarchy, spacing, responsive behavior, component consistency, interaction states, and system fit. This is for UI craft and component execution; use `UX Flow Polish.md` for journey continuity, `Product Copy Polish.md` for microcopy-heavy work, and `Design System Polish.md` for shared token/component ownership.

## Scope selection

- If the user named a page, component, route, breakpoint, visual bug, or design drift, polish that surface and directly affected states.
- If the request is broad, inspect primary reachable UI surfaces and select the highest-confidence improvement with visible user impact.
- Include related state, a11y, copy, and test updates when they are part of the same surface quality problem.
- Avoid full redesigns, brand changes, new component libraries, dependency changes, and backend behavior changes unless the UI fix requires them.

## Polish targets

- Visual hierarchy: section grouping, density, alignment, spacing, typography scale, CTA prominence, scan order, and affordances.
- Responsive behavior: breakpoint-specific layout, overflow/clipping, table/card fallback, sticky/fixed elements, safe areas, and mobile touch targets.
- Component consistency: variants, sizes, icon placement, token usage, ad-hoc styles, duplicated markup, and mixed visual languages.
- Interaction states: hover/focus/active/pressed/disabled/loading/skeleton/error/empty/success/destructive/no-access/no-plan/over-quota.
- Media and assets: icon semantics, image sizing, alt text where user-visible, aspect ratios, fallback states, and asset reuse.
- Directly affected tests, snapshots, stories, screenshots, docs, and localization catalogs when the repo uses them.

## Implementation principles

- Reuse existing components, tokens, layout primitives, theme config, CSS conventions, and i18n architecture.
- Fix the owner component or route-level pattern instead of scattering local visual workarounds.
- Preserve current behavior unless a visual/system mismatch creates a user-facing defect.
- Keep copy truthful and concise, but do not turn this prompt into a marketing rewrite.

## Validation

Run relevant repository-native checks. Use preview, Storybook, screenshot, or Playwright tooling when available; otherwise state the limitation. When explaining non-obvious repo facts or skipped adjacent work, cite `path:line[-line]`.

## Final response

Respond in Russian with compact emoji sections: ♻️ changed UI surface, 📁 key files, 🔎 evidence anchors when relevant, 🧪 checks, 👀 visual/manual review, ⚠️ assumptions/risks, ⛔ not run/not included.
