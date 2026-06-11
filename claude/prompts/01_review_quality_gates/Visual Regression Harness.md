# Visual Regression Harness

## Mode

- Use the active `CLAUDE.md` context if present, then repository evidence.
- Work in the current Claude Code Cloud session. Do not assume hidden background runs or extra delegation mechanisms unless the user explicitly provides them.
- Implementation/documentation mode: add or improve one repository-native visual regression or screenshot review path when current evidence justifies it.

## Goal

Create a small, maintainable visual validation loop for one high-value UI surface or component family. The result should be runnable with existing repo tooling and should catch meaningful visual/state regressions without turning CI into a flaky screenshot farm.

## Scope selection

- If the user named a route, component, story, screenshot gap, or UI audit work item, target that surface and its critical states.
- If the request is broad, inspect existing preview/test tooling and choose one high-confidence UI path with frequent changes or high user impact.
- Prefer extending existing Playwright/Storybook/component test patterns over introducing new tools.
- Avoid broad visual baselines, pixel-perfect coverage for unstable surfaces, new hosting services, and dependency changes unless the repo already supports them or the task requires them.

## Harness targets

- Critical states: default, loading, empty, error, disabled/no-access/no-plan, destructive confirmation, responsive/mobile, and high-risk variants.
- Stable setup: deterministic test data, mocked network where repo-standard, seeded state, fixed viewport, stable dates/randomness, and hidden animation where existing tooling supports it.
- Reviewability: clear screenshot artifact names, focused assertions, documented command, and failure output that helps reviewers inspect the changed surface.
- Maintenance: small number of high-signal screenshots, nearby fixtures, no brittle pixel assertions where semantic assertions are better.

## Implementation principles

- Use repository-native scripts, test framework, preview server, and fixtures.
- Keep the harness local to the selected surface unless a shared helper is clearly warranted.
- Do not claim visual verification unless screenshots/previews were actually generated or tests ran.
- Update docs or package scripts when the repo pattern expects discoverable commands.

## Validation

Run the new or changed visual check when possible. If browser/preview dependencies cannot run, validate static wiring and state the exact limitation.

## Final response

Respond in Russian with compact emoji sections: ✅ harness result, 📁 key files, 🔎 selected surface evidence, 🧪 checks, 👀 artifact/manual review path, ⚠️ assumptions/risks, ⛔ not run/not included.
