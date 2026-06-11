# Reliability Polish

## Mode

- Use the active `AGENTS.md` chain.
- Execute mode: edit the repository only for the selected owner-layer slice and directly affected validation/docs.

## Goal

Implement one selected reliability fix at the owner layer without broad redesign, making failure handling explicit, safe, observable, and validated.

## Relation to existing prompts

Use this prompt after a concrete reliability issue has been selected and the fix belongs at an owner layer such as timeout, retry, degraded mode, recovery, readiness, or diagnostics contract. If the change is only adding logs/metrics/runbooks without changing reliability behavior, use `08_infra_ops_jobs/Observability Polish.md`. If the selected slice is only a queue, worker, cron, or webhook lifecycle, use `08_infra_ops_jobs/Background Jobs Polish.md`.

## Inspect

The selected failure path, its owner layer, direct callers/consumers, config/env, retry/timeout/idempotency behavior, user-facing errors, logs/metrics, tests, docs/runbooks, and deploy/runtime contracts.

## Focus areas

- Add or tighten timeout/cancellation/deadline behavior using existing repo patterns.
- Make retry/backoff/idempotency behavior explicit and safe for the affected side effect.
- Introduce a bounded degraded mode only when repo evidence supports safe fallback semantics.
- Make startup/readiness/shutdown behavior reflect actual dependency availability.
- Add durable recovery, dead-letter, reconciliation, or operator diagnostics for the selected path when the repo has the seam for it.
- Update tests/docs/config examples for the changed reliability contract.

## Implementation principles

- Fix the selected behavior at the owning layer/source of truth, not only at the visible symptom.
- Keep the diff focused: update direct callers, tests, docs, config, generated artifacts, and runtime contracts only when affected.
- Do not add hidden fallbacks, broad catch blocks, silent retries, speculative flags, new frameworks, or broad abstractions unless repository evidence requires them.
- Preserve existing public/internal contracts unless the selected fix explicitly requires a contract change; update consumers when contracts change.
- Make failure, consistency, idempotency, and performance behavior explicit enough to test or observe.
- Do not log secrets, raw tokens, raw PII, private documents, prompts, or user-visible stack traces.

## Validation

Run repository-native checks for the changed slice. Prefer tests that exercise the owner invariant or hot path, then directly affected integration/build/type checks. If a check cannot run, state the concrete limitation.

## Final response

Respond in Russian with compact emoji sections: ✅ result, ♻️ changed scope, 📁 key files, 🔎 evidence anchors, 🧪 checks, 👀 manual trace, ⚠️ assumptions/risks, ⛔ not run/not included.
