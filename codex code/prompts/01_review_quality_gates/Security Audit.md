# Security Audit

## Mode

- Use the active `AGENTS.md` chain.
- Plan mode only: inspect the repository, do not edit product code.

## Goal

Find reachable security issues with concrete repository evidence and produce remediation task-subs. Do not inflate theoretical patterns into vulnerabilities.

## Inspect

Authentication, sessions, cookies, token handling, authorization policies, tenant/project scoping, admin/staff paths, input validation, serializers, uploads, webhooks, external calls, redirects, secrets/config, logging, migrations, database access, rate limiting, CI/deploy files, and tests.

## Security classes

Look for concrete, reachable issues in:

- Authn/session lifecycle: login, logout, refresh, password reset, OAuth/callbacks, CSRF/CORS, cookie flags, token expiry/storage.
- Authz/RBAC/ABAC: role checks, tenant/workspace/project isolation, object-level access, staff/admin bypasses, visible actions vs allowed actions.
- Injection and unsafe parsing: SQL/NoSQL/command/template injection, SSRF, path traversal, unsafe deserialization, unsafe regex, XML/entity handling.
- Web/API exposure: open redirect, missing webhook signature verification, replay/idempotency gaps, upload MIME/size/path handling, public error leakage.
- Secrets and config: hardcoded secrets, secret logging, weak defaults, missing required env validation, production debug behavior.
- Data protection: PII leakage, excessive logging, export/import exposure, destructive actions without guardrails, backup/migration risks.
- Abuse controls: rate limits, quota bypass, brute-force paths, spam/proactive messaging, background job amplification.
- Dependency/deploy risk only when the repo exposes the vulnerable package/config/path or CI/deploy behavior makes it reachable.

## Priority model

### P0

Reachable unauthorized access, tenant/data leakage, credential/session compromise, payment/webhook trust failure, destructive action abuse, secret exposure, or direct injection path.

### P1

Meaningful defense gap in an important flow, inconsistent authorization, insufficient boundary validation, weak rate limiting, sensitive logging, or missing security test for critical behavior.

### P2

Lower-risk hardening with current reachability: misleading security config, weak diagnostics boundary, partial policy drift, or documented-but-not-enforced constraint.

## Task-sub quality

- Use native Codex Cloud task-sub creation when available; do not force a handmade markdown task-sub body.
- Every task-sub must cite `path:line[-line]` evidence for the problematic behavior/contract and the owner layer, plus symbol when possible.
- Include reachable surface, affected actors/consumers/states, expected behavior, acceptance criteria, and validation direction when discoverable.
- Use one unambiguous fix direction per task-sub; no alternatives.
- Merge symptoms under the same behavior owner/source of truth unless fixes, rollout units, or validation differ.
- Do not report theoretical risks, stylistic preferences, or generic best practices without current repo impact.
- Distinguish direct repo evidence from exploitability inference.
- Prefer fixes at the owning boundary/policy layer over duplicated local guards.
- Do not include exploit payloads beyond what is necessary to explain the risk.

## Output contract

Produce only native Codex Cloud task-subs grouped by P0/P1/P2. If none qualify, output each priority with `None`. Do not print a custom task-sub schema.
