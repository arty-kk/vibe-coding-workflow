# Consistency Guard Polish

## Mode

- Use the active `AGENTS.md` chain.
- Execute mode: edit the repository only for the selected owner-layer slice and directly affected validation/docs.

## Goal

Implement one selected consistency fix by moving or tightening the source of truth, removing drift, and adding guard validation where the repository pattern supports it.

## Relation to existing prompts

Use this prompt after selecting one invariant drift issue that needs an owner/source-of-truth fix and directly affected consumers updated. If the selected issue is a permission, role, session, or tenant boundary, use `09_business_rules_data_analytics/Auth Permissions Polish.md`. If it is a plan, quota, subscription, or billing-provider entitlement rule, use `09_business_rules_data_analytics/Billing Entitlements Polish.md`. If it is a larger migration/refactor without a single invariant owner, use `10_docs_refactor_generation/Migration & Refactor.md` only when that prompt better matches the scope.

## Inspect

The rule/invariant owner, duplicated implementations, call sites, API/schema/generated types, UI gates, storage constraints, migrations, cache invalidation, jobs, tests, fixtures, docs, and migration/backfill needs.

## Focus areas

- Replace duplicate rule checks with a shared owner or generated contract already consistent with repo architecture.
- Add boundary validation, type narrowing, database constraints, or state-transition guards at the layer that owns the invariant.
- Update direct consumers, generated artifacts, fixtures, examples, and docs that would otherwise drift.
- Fix cache/projection invalidation or repair path for the selected invariant.
- Preserve backward compatibility only when repo evidence requires it; otherwise remove replaced drift paths.
- Add tests for the invariant owner and the most important consumer boundary.

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
