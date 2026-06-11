# Performance Audit

## Mode

- Use the active `AGENTS.md` chain.
- Plan mode only: inspect the repository, do not edit product code.

## Goal

Find reachable performance problems that affect user experience, throughput, cost, reliability, or operational stability. Keep issues where current repository evidence shows a concrete hot path or high-risk path.

## Inspect

Routes/pages/components, handlers/services, database queries, migrations/indexes, caches, background jobs, queues, external calls, build/bundle config, assets, SSR/ISR/static generation, telemetry, tests/benchmarks, CI, and docs.

## Issue classes

Look for concrete, reachable issues in:

- Database: N+1 queries, missing indexes for common filters/joins/sorts, unbounded scans, transaction scope, pagination/cursor inefficiency.
- API/server: blocking I/O, serial external calls, synchronous heavy work in request path, missing caching for stable expensive data, retry storms.
- Frontend: unnecessary client waterfalls, bundle bloat, heavy hydration, repeated expensive renders, large assets, missing lazy loading where repo patterns support it.
- Background jobs: duplicate work, unbounded queues, inefficient polling, non-idempotent retries, job amplification.
- Build/deploy/runtime: cold-start cost, memory spikes, cache invalidation drift, health checks that mask degraded service.
- Observability/testing: performance assumptions contradicted by code, missing guard tests/benchmarks for a critical path when a harness exists.

## Priority model

### P0

Performance issue that can cause outage, data loss, severe critical-path failure, request collapse, or runaway cost in a reachable production path.

### P1

Hot-path latency/cost/reliability issue with clear user or operational impact.

### P2

Lower-risk but real inefficiency that affects maintainability, future scaling, or a non-critical but reachable path.

## Task-sub quality

- Use native Codex Cloud task-sub creation when available; do not force a handmade markdown task-sub body.
- Every task-sub must cite `path:line[-line]` evidence for the problematic behavior/contract and the owner layer, plus symbol when possible.
- Include reachable surface, affected actors/consumers/states, expected behavior, acceptance criteria, and validation direction when discoverable.
- Use one unambiguous fix direction per task-sub; no alternatives.
- Merge symptoms under the same behavior owner/source of truth unless fixes, rollout units, or validation differ.
- Do not report theoretical risks, stylistic preferences, or generic best practices without current repo impact.
- Explain impact from repo-visible reachability and mark inferred traffic/scale assumptions clearly.
- Prefer owner-layer fixes: query/index/pagination/caching/job structure/source-of-truth, not cosmetic local tweaks.
- If validation commands/benchmarks are absent, specify observable checks that an execute run can add or perform.

## Output contract

Produce only native Codex Cloud task-subs grouped by P0/P1/P2. If none qualify, output each priority with `None`. Do not print a custom task-sub schema.
