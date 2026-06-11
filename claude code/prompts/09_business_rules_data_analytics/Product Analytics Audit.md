# Product Analytics Audit

## Mode

- Use the active `CLAUDE.md` context if present, then repository evidence.
- Work in the current Claude Code Cloud session. Do not assume hidden background runs or extra delegation mechanisms unless the user explicitly provides them.
- Analysis-only mode: inspect the repository, do not edit product code.

## Goal

Audit product analytics and instrumentation quality for existing user/product flows: event taxonomy, firing points, properties, privacy, deduplication, funnel usefulness, tests, and docs. Keep only issues supported by repository evidence; do not recommend adding a new vendor unless the repo already has an explicit direction.

## Inspect

Analytics wrappers, telemetry clients, event constants/types, server/client tracking calls, consent/privacy gates, route/action handlers, feature flags, auth/session/tenant context, onboarding/payment/core flows, docs, tests, dashboards/config if committed, and observability conventions.

## Issue classes

Look for concrete, reachable issues in:

- Event taxonomy: duplicated event names, inconsistent properties, no source of truth, unstable IDs, missing tenant/plan/context where safe and necessary.
- Firing correctness: events fire before success, miss failure/cancel states, double-fire on rerender/retry, omit server-confirmed outcomes, or cannot distinguish user intent from system effect.
- Funnel coverage: critical steps in signup/onboarding/billing/core workflow are unmeasurable with existing patterns.
- Privacy and consent: PII/secrets logged, excessive payloads, analytics before consent where the repo models consent, unsafe diagnostic data, or cross-tenant leakage risk.
- Regression resistance: no tests/types/docs for critical events, stale event docs, fragile wrappers, or instrumentation coupled to UI implementation details.
- Operational signal: important product failures lack safe correlation with logs/metrics where the repo already has patterns.

## Priority model

### P0

Analytics/instrumentation leaks sensitive data, violates tenant/privacy boundaries, corrupts billing/security-relevant auditability, or causes production instability.

### P1

Critical funnel/core behavior cannot be measured, fires incorrectly, duplicates materially, or lacks type/test protection on high-value paths.

### P2

Lower-risk but concrete event cleanup: inconsistent naming, missing docs, weak properties, secondary flow gaps, or maintainability issues in wrappers.

## Work item quality

- Output findings as compact chat work items; do not assume a platform-specific task workflow or extra delegation mechanism.
- Each work item must cite `path:line[-line]` evidence for event owner/wrapper and affected flow.
- Include expected event semantics, privacy boundary, acceptance criteria, and validation direction.
- Merge issues by event owner or flow when one fix validates them together.

## Output contract

Produce chat work items grouped by P0/P1/P2. If none qualify, output each priority with `None`. Use compact chat bullets; do not force a rigid work-item schema.
