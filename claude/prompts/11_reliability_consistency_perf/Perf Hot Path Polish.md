# Perf Hot Path Polish

## Mode

- Use the active `CLAUDE.md` context if present, then repository evidence.
- Work in the current Claude Code Cloud session. Do not assume hidden background runs or extra delegation mechanisms unless the user explicitly provides them.
- Implementation mode: edit the repository only for the selected owner-layer slice and directly affected validation/docs.

## Goal

Implement one selected hot-path performance fix with a clear owner-layer change, measurable validation, and no speculative broad optimization.

## Relation to existing prompts

Use this prompt after `01_review_quality_gates/Performance Audit.md` or `11_reliability_consistency_perf/Performance Budget Audit.md` identifies one concrete hot-path fix to implement. Do not use it for broad performance discovery, release readiness, or unrelated cleanup. If the selected bottleneck is entirely inside a background worker lifecycle, prefer `08_infra_ops_jobs/Background Jobs Polish.md`.

## Inspect

The hot path entry point, data fetch/query plan, rendering/server boundary, provider fanout, cache/invalidation contract, assets/bundle config, existing telemetry/benchmarks, tests, and directly affected docs.

## Focus areas

- Remove N+1 or serial fanout by changing the owner data access/service boundary.
- Bound cardinality with pagination, chunking, streaming, batching, indexing, or caching consistent with repo patterns.
- Move expensive work out of a request/render path only when correctness, idempotency, and observability remain explicit.
- Reduce bundle/asset/render cost without changing UX contracts.
- Add a regression guard through existing tests, benchmark scripts, CI, or observable metrics.
- Document the performance contract when the repo already documents similar operational limits.

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
