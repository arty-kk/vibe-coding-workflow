# Performance Audit

## Mode

- Use the active `CLAUDE.md` context if present, then repository evidence.
- Work in the current Claude Code Cloud session. Do not assume hidden background runs or extra delegation mechanisms unless the user explicitly provides them.
- Analysis-only mode: inspect the repository, do not edit product code.

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

## Work item quality

- Output findings as compact chat work items; do not assume a platform-specific task workflow or extra delegation mechanism.
- Each work item must cite `path:line[-line]` evidence for the problematic behavior/contract and the owner layer, plus symbol when possible.
- Include reachable surface, affected actors/consumers/states, expected behavior, acceptance criteria, and validation direction when discoverable.
- Use one unambiguous fix direction per work item; no alternatives.
- Merge symptoms under the same behavior owner/source of truth unless fixes, rollout units, or validation differ.
- Do not report theoretical risks, stylistic preferences, or generic best practices without current repo impact.
- Explain impact from repo-visible reachability and mark inferred traffic/scale assumptions clearly.
- Prefer owner-layer fixes: query/index/pagination/caching/job structure/source-of-truth, not cosmetic local tweaks.
- If validation commands/benchmarks are absent, specify observable checks that an implementation pass can add or perform.

## Output contract

Produce chat work items grouped by P0/P1/P2. If none qualify, output each priority with `None`. Use compact chat bullets; do not force a rigid work-item schema.
