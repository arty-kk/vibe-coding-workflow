# Idempotency Concurrency Audit

## Mode

- Use the active `AGENTS.md` chain.
- Plan mode only: inspect the repository, do not edit product code.

## Goal

Find reachable bugs caused by duplicate delivery, concurrent requests, out-of-order events, worker restarts, partial retries, or optimistic UI/server races.

## Relation to existing prompts

Use this prompt for duplicate delivery, races, replay, and transaction-boundary hazards in mutating flows that may span UI/API, webhooks, jobs, storage, and external side effects. If the risk is confined to worker/queue/cron lifecycle, use `08_infra_ops_jobs/Background Jobs Audit.md`. If the risk is confined to billing lifecycle, quotas, or provider webhooks, use `09_business_rules_data_analytics/Billing Entitlements Audit.md`. If the risk appears only in a current diff, use `11_reliability_consistency_perf/Reliability Consistency Perf Patch Check.md`.

## Inspect

Mutating API endpoints, forms/actions, payment/billing flows, webhooks, jobs, queues, schedulers, import/export flows, file processing, notifications, transaction scopes, locks, uniqueness constraints, idempotency keys, tests, and provider docs pinned by the repo.

## Focus areas

- Duplicate submission or delivery creates duplicate rows, charges, emails, jobs, files, notifications, grants, or irreversible side effects.
- Race conditions around check-then-act, quota/entitlement consumption, inventory/capacity limits, balance updates, status changes, lock acquisition, and uniqueness assumptions.
- Out-of-order or replayed events regress state, resurrect deleted data, overwrite newer values, or skip compensation.
- Transactions do not cover the invariant they claim to protect, or side effects occur inside/outside transaction boundaries in an unrecoverable order.
- Optimistic UI, background refresh, or realtime updates can show committed states that the owner layer does not actually guarantee.
- Missing replay, dedupe, dead-letter, reconciliation, or audit trail where the repo already has a pattern or where the operation is high impact.

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
