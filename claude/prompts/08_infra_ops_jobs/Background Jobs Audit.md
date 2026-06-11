# Background Jobs Audit

## Mode

- Use the active `CLAUDE.md` context if present, then repository evidence.
- Work in the current Claude Code Cloud session. Do not assume hidden background runs or extra delegation mechanisms unless the user explicitly provides them.
- Analysis-only mode: inspect the repository, do not edit product code.

## Goal

Audit background work: queues, workers, cron/scheduled jobs, webhooks, retries, idempotency, locks, concurrency, long-running tasks, cleanup, and observability. Keep only repository-visible issues with correctness, data, cost, reliability, or operational impact.

## Inspect

Queue/job definitions, worker entry points, schedulers/cron, webhook handlers, retry/backoff logic, idempotency keys, locks/transactions, batch/pagination loops, migrations, config/env, deployment/CI, logs/metrics/traces, dead-letter handling, admin tooling, tests, docs, and related API/UI state.

## Issue classes

Look for concrete, reachable issues in:

- Correctness and idempotency: duplicate processing, unsafe retries, missing dedupe, out-of-order webhooks, non-atomic state transitions, partial writes, and inconsistent cleanup.
- Concurrency and scale: missing locks, race-prone counters/quotas, unbounded fan-out, memory/time limits, N+1 batch work, starvation, and thundering herd patterns.
- Failure handling: swallowed errors, infinite retries, no dead-letter/poison handling where architecture expects it, poor recovery path, and user-visible state stuck pending.
- Operational readiness: missing health/metrics/log context, unsafe secrets/config, deploy ordering issues, migrations required before workers, and lack of runbook for critical jobs.
- Data/privacy safety: cross-tenant processing, PII leakage in logs/payloads, retention cleanup gaps, and destructive job without guardrails.
- Regression resistance: missing tests/fixtures for retries/idempotency/lifecycle edges, stale docs, or workers not exercised by CI.

## Priority model

### P0

Job can corrupt/delete data, leak cross-tenant/private data, charge/send/notify repeatedly, deadlock critical production work, or break billing/security lifecycle.

### P1

Important idempotency/retry/concurrency gap, stuck pending user state, missing observability for critical worker, or missing tests for high-risk background behavior.

### P2

Lower-risk but concrete job quality issue: stale runbook, weak logging, minor batch inefficiency, secondary retry gap, or maintainability issue in worker ownership.

## Work item quality

- Output findings as compact chat work items; do not assume a platform-specific task workflow or extra delegation mechanism.
- Each work item must cite `path:line[-line]` evidence for producer, worker, state owner, and affected consumer when possible.
- Include expected lifecycle behavior, failure/retry/idempotency contract, acceptance criteria, and validation direction.
- Merge issues by job owner when one fix validates them together.

## Output contract

Produce chat work items grouped by P0/P1/P2. If none qualify, output each priority with `None`. Use compact chat bullets; do not force a rigid work-item schema.
