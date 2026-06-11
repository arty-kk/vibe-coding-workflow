# Security Audit

## Mode

- Use the active `CLAUDE.md` context if present, then repository evidence.
- Work in the current Claude Code Cloud session. Do not assume hidden background runs or extra delegation mechanisms unless the user explicitly provides them.
- Analysis-only mode: inspect the repository, do not edit product code.

## Goal

Find reachable security issues with concrete repository evidence and produce remediation work items. Do not inflate theoretical patterns into vulnerabilities.

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

## Work item quality

- Output findings as compact chat work items; do not assume a platform-specific task workflow or extra delegation mechanism.
- Each work item must cite `path:line[-line]` evidence for the problematic behavior/contract and the owner layer, plus symbol when possible.
- Include reachable surface, affected actors/consumers/states, expected behavior, acceptance criteria, and validation direction when discoverable.
- Use one unambiguous fix direction per work item; no alternatives.
- Merge symptoms under the same behavior owner/source of truth unless fixes, rollout units, or validation differ.
- Do not report theoretical risks, stylistic preferences, or generic best practices without current repo impact.
- Distinguish direct repo evidence from exploitability inference.
- Prefer fixes at the owning boundary/policy layer over duplicated local guards.
- Do not include exploit payloads beyond what is necessary to explain the risk.

## Output contract

Produce chat work items grouped by P0/P1/P2. If none qualify, output each priority with `None`. Use compact chat bullets; do not force a rigid work-item schema.
