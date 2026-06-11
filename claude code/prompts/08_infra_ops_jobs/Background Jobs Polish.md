# Background Jobs Polish — Queues, Cron, Retries, and Idempotency

## Mode

- Use the active `CLAUDE.md` context if present, then repository evidence.
- Work in the current Claude Code Cloud session. Do not assume hidden background runs or extra delegation mechanisms unless the user explicitly provides them.
- Implementation mode: change the repository when a focused background-job improvement is justified by current evidence.

## Goal

Improve one coherent async workflow end to end: enqueue trigger, payload contract, worker execution, idempotency, retries, failure recovery, observability, and user/admin visibility where relevant.

## Scope selection

- If the user named a worker, queue, cron, webhook, ingestion, email, export, sync, billing, or AI/OCR/RAG job, polish that async path and directly affected producers/consumers.
- If the request is broad, inspect background seams and apply the highest-confidence improvement with reliability, data-integrity, or operator-impact value.
- Include related schema, locking, status UI, logs/metrics, tests, and docs when they belong to the same job contract.
- Avoid queue provider migrations, broad scheduler rewrites, and unrelated worker cleanup unless required by the selected fix.

## Polish targets

- Job contract: payload schema, stable IDs, versioning, tenant/user/project scope, dedupe keys, trace IDs, and producer/consumer compatibility.
- Execution safety: idempotency, transaction boundaries, locks, concurrency limits, cancellation, timeout, retry/backoff, poison/dead-letter handling, and partial failure recovery.
- Side effects: emails/webhooks/payments/imports/exports/indexing/cache invalidation with duplicate prevention and replay safety.
- Visibility: status fields, admin/user feedback, logs, metrics, traces, alert hooks, and safe diagnostics.
- Tests: unit/integration fixtures for success, retry, duplicate, failure, permission/scope, stale payload, and recovery paths.

## Implementation principles

- Make retries safe before making them more aggressive.
- Keep payloads minimal, explicit, and validated at the worker boundary.
- Prefer owner-layer domain operations over worker-local business logic forks.
- Preserve existing queue/scheduler abstractions and deployment assumptions.
- Update directly affected tests, fixtures, docs, and generated maps when the repo uses them.

## Validation

Run repository-native checks for the touched job path. Prefer tests or local commands that exercise enqueue and worker execution. If the queue provider, cron runtime, or credentials are unavailable, state the exact unverified runtime behavior and manual validation path.

## Final response

Respond in Russian with compact emoji sections: ♻️ changed async path, 📁 key files, 🔎 evidence anchors, 🧪 checks, 👀 job trace, ⚠️ assumptions/risks, ⛔ not run/not included.
