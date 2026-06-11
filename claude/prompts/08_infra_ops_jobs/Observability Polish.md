# Observability Polish — Logs, Metrics, Health, and Runbooks

## Mode

- Use the active `CLAUDE.md` context if present, then repository evidence.
- Work in the current Claude Code Cloud session. Do not assume hidden background runs or extra delegation mechanisms unless the user explicitly provides them.
- Implementation mode: change the repository when a focused observability or operability improvement is justified by current evidence.

## Goal

Improve one coherent operational surface so failures become diagnosable and safe to act on without leaking internals or sensitive data. The diff should add meaningful signal, not noisy logging.

## Scope selection

- If the user named a flow, job, endpoint, deploy path, incident class, or missing signal, polish that operational surface and directly affected runtime states.
- If the request is broad, inspect current operational surfaces and choose the highest-confidence improvement with release, reliability, or support impact.
- Include related health checks, runbook notes, tests, config docs, and safe diagnostics when they belong to the same operational behavior.
- Avoid introducing new vendors, agents, dependencies, or broad telemetry frameworks unless the repo already uses them or the task requires it.

## Polish targets

- Structured logs with correlation/request/job identifiers, safe error categories, and operator-actionable context.
- Metrics/counters/timers around critical success/failure states, queue/job outcomes, retries, rate limits, external calls, and degraded modes.
- Health/readiness checks that reflect real dependencies without exposing sensitive diagnostics publicly.
- Runbooks and env/config docs for alertable failure modes, deploy/migration recovery, and manual verification.
- Tests or script checks for changed diagnostics where the repo has a pattern.

## Implementation principles

- Reuse existing logging, metrics, tracing, config, and health-check patterns.
- Do not log secrets, raw tokens, raw PII, full private documents, model prompts, or stack traces to user-visible surfaces.
- Prefer owner-layer instrumentation over scattered local logs.
- Keep user-facing errors safe and concise; keep operator diagnostics in server-side logs/telemetry.
- Update directly affected docs, env examples, and tests when the repo uses them.

## Validation

Run relevant repository-native checks. When feasible, run or simulate the changed path enough to confirm the new signal is emitted and sensitive values are not printed.

## Final response

Respond in Russian with compact emoji sections: ♻️ changed operational surface, 📁 key files, 🔎 evidence anchors, 🧪 checks, 👀 manual trace, ⚠️ assumptions/risks, ⛔ not run/not included.
