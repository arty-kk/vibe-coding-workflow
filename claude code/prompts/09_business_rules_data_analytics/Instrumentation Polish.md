# Instrumentation Polish — Events, Telemetry, Logs, and Product Signals

## Mode

- Use the active `CLAUDE.md` context if present, then repository evidence.
- Work in the current Claude Code Cloud session. Do not assume hidden background runs or extra delegation mechanisms unless the user explicitly provides them.
- Implementation mode: change the repository when a focused instrumentation improvement is justified by current evidence.

## Goal

Improve one coherent instrumentation surface so product behavior, failures, or operational states become measurable and safe to diagnose. Use existing analytics/telemetry/logging patterns; do not add a new vendor unless the repository already standardizes that path and the task requires it.

## Scope selection

- If the user named a flow, event, metric, log gap, dashboard contract, or analytics audit work item, improve that owner and directly affected calls.
- If the request is broad, inspect high-impact flows and choose the highest-confidence signal improvement with product, reliability, or support value.
- Include related tests, docs, types, privacy guards, and user-facing state correlation when they belong to the same signal.
- Avoid noisy logging, PII capture, speculative dashboards, broad observability rewrites, and unrelated refactors.

## Polish targets

- Product events: names, typed properties, stable IDs, tenant/plan/context where safe, success/failure/cancel timing, dedupe, and funnel continuity.
- Operational telemetry: safe logs, counters/timers, spans/traces, health diagnostics, job/retry signals, and correlation IDs where existing patterns support them.
- Privacy and safety: consent gates, PII minimization, redaction, secret avoidance, and user-safe diagnostics.
- Regression resistance: event constants/types, tests, docs, fixtures, snapshot updates, and wrapper-level validation.
- User-flow alignment: events should reflect completed behavior, not just UI clicks, unless the existing taxonomy explicitly separates intent and outcome.

## Implementation principles

- Reuse existing wrappers, event schemas, logger/metrics clients, feature flags, and config conventions.
- Prefer owner-layer instrumentation over scattered UI-only calls when behavior is confirmed server-side.
- Keep payloads small, stable, and privacy-safe.
- Do not claim analytics is verified unless checks or repo-local tests actually ran.

## Validation

Run relevant repository-native checks. When possible, trace one success and one failure/cancel path for the instrumented behavior. State any inability to verify external dashboards or vendors.

## Final response

Respond in Russian with compact emoji sections: ♻️ changed instrumentation, 📁 key files, 🔎 evidence anchors, 🧪 checks, 👀 signal trace, ⚠️ assumptions/risks, ⛔ not run/not included.
