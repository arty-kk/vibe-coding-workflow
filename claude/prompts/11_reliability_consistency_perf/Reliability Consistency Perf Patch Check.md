# Reliability Consistency Perf Patch Check

## Mode

- Use the active `CLAUDE.md` context if present, then repository evidence.
- Work in the current Claude Code Cloud session. Do not assume hidden background runs or extra delegation mechanisms unless the user explicitly provides them.
- Review-only mode: inspect the current diff and affected repository evidence, do not edit product code.

## Goal

Review the current diff for regressions in reliability, consistency, idempotency, concurrency, performance budgets, and observability before merge.

## Relation to existing prompts

Use this as a narrow supplemental patch review when the current diff touches reliability, invariants, idempotency/concurrency, performance budgets, or observability/security failure modes. For the default comprehensive patch check that can also apply fixes, use `01_review_quality_gates/Patch Checking.md`. For ship/no-ship readiness across an entire feature or release, use `01_review_quality_gates/Release Readiness Audit.md`.

## Inspect

The current diff plus affected owners, callers, tests, configs, generated artifacts, migrations, docs, runtime contracts, and any changed deploy/job/provider surfaces.

## Focus areas

- Reliability: new unbounded waits, unsafe retries, hidden fallbacks, swallowed errors, readiness/health drift, or failure paths without diagnostics.
- Consistency: duplicated rules, schema/type/API drift, cache invalidation gaps, invalid states, missed generated artifacts, or doc/test fixture drift.
- Idempotency/concurrency: duplicate side effects, races, transaction boundary gaps, missing dedupe keys, replay hazards, or out-of-order state regressions.
- Performance: unbounded cardinality, added waterfalls, heavier bundles/assets, inefficient queries, provider/model cost amplification, or missing regression guard.
- Observability/security: secret/PII leakage in logs, missing correlation for new failure modes, or user-facing internal diagnostics.
- Validation: tests that do not exercise the changed contract, fake confidence, or skipped necessary checks without an explicit limitation.

## Priority model

### P0

Issue that can cause outage, data loss, duplicate irreversible side effects, tenant/privacy breach, severe critical-path failure, request collapse, or runaway cost in a reachable production path.

### P1

Hot-path reliability, consistency, concurrency, or performance issue with clear user, business, operational, or cost impact.

### P2

Lower-risk but real issue that affects maintainability, future scaling, diagnosability, or a non-critical but reachable path.

## Review rules

- Ground every issue in the current diff plus affected repository evidence.
- Cite `path:line[-line]` evidence for the changed code and the owner/consumer contract it affects, plus symbol when possible.
- Distinguish regression introduced by the diff from pre-existing risk.
- Do not request unrelated cleanup, broad redesign, or speculative hardening.
- Merge duplicate symptoms under the same owner-layer fix.
- Include validation direction for each finding and list checks that were inspected or should be run.

## Output contract

Respond in Russian with actionable P0/P1/P2 review findings as compact chat work items. If no regressions qualify, output `No actionable reliability/consistency/performance regressions found` plus the checks/evidence reviewed.
