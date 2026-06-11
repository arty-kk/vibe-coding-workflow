# Performance Budget Audit

## Mode

- Use the active `AGENTS.md` chain.
- Plan mode only: inspect the repository, do not edit product code.

## Goal

Find concrete performance-budget risks and regression gaps in hot paths, especially where latency, throughput, memory, bundle size, database cost, provider cost, or job duration can grow without a guardrail.

## Relation to existing prompts

Use this prompt to define, verify, or enforce measurable performance budgets and regression guardrails for a known hot path. For broad discovery of reachable performance defects, use `01_review_quality_gates/Performance Audit.md` first. For release-blocking readiness across tests, deploy, rollback, observability, security, docs, and product states, use `01_review_quality_gates/Release Readiness Audit.md`. For implementing one selected hot-path fix, use `11_reliability_consistency_perf/Perf Hot Path Polish.md`.

## Inspect

Hot routes/pages/actions, rendering boundaries, data fetching, database queries/indexes, API fanout, caches, job loops, provider/model calls, assets, bundling, CI, existing benchmarks, logs/metrics, SLO docs, and release checks.

## Focus areas

- No explicit or testable budget for a repo-visible hot path where the code already implies a latency/size/cost expectation.
- Unbounded input/output cardinality: page sizes, loops, query result sets, job batches, exports, OCR/RAG/model chunks, assets, or in-memory aggregation.
- Waterfalls and fanout: serial awaits, N+1 provider/database calls, repeated expensive renders, cache misses, or avoidable round trips.
- Memory and artifact growth: retained buffers, full-file loads, large bundle chunks, uncompressed assets, or generated artifacts that scale with user data.
- Cost amplification: model/provider calls, retries, polling, cron overlap, background reprocessing, or analytics/events that scale faster than the user action.
- Regression visibility gaps: missing benchmark/test/CI/log metric where an existing harness could enforce the hot-path budget.

## Priority model

### P0

Issue that can cause outage, data loss, duplicate irreversible side effects, tenant/privacy breach, severe critical-path failure, request collapse, or runaway cost in a reachable production path.

### P1

Hot-path reliability, consistency, concurrency, or performance issue with clear user, business, operational, or cost impact.

### P2

Lower-risk but real issue that affects maintainability, future scaling, diagnosability, or a non-critical but reachable path.

## Evidence rules

- Keep only concrete, reachable findings supported by current repository evidence.
- Cite `path:line[-line]` evidence for the problematic behavior/contract and the owner layer, plus symbol when possible.
- Distinguish direct repository facts from assumptions about traffic, scale, deployment, users, providers, or operations.
- Merge symptoms under the same owner/source of truth unless fixes, rollout units, or validation differ.
- Prefer owner-layer fixes over local guards, cosmetic rewrites, broad catch blocks, or hidden fallbacks.
- Do not report generic best practices, hypothetical scale concerns, or style preferences without repo-visible reachability.

## Work item quality

- Use native Codex Cloud task-sub creation when available; do not force a handmade markdown task-sub body.
- Every task-sub must include affected surface, actors/consumers/states, expected behavior, acceptance criteria, and validation direction when discoverable.
- Use one unambiguous fix direction per task-sub; no alternatives.
- If validation commands or harnesses are absent, specify observable checks that an execute run can add or perform.

## Output contract

Produce only native Codex Cloud task-subs grouped by P0/P1/P2. If none qualify, output each priority with `None`. Do not print a custom task-sub schema.
