# API Audit

## Mode

- Use the active `CLAUDE.md` context if present, then repository evidence.
- Work in the current Claude Code Cloud session. Do not assume hidden background runs or extra delegation mechanisms unless the user explicitly provides them.
- Analysis-only mode: inspect the repository, do not edit product code.

## Goal

Audit the reachable API surface for behavior, contract, validation, security-adjacent, and integration defects. Keep only issues supported by current repository evidence.

## Inspect

- Route definitions, controllers/handlers/resolvers, middleware, auth guards, policies, schemas/DTOs, serializers, validators, generated clients, OpenAPI/GraphQL/RPC docs, tests, migrations/models, and consumers.
- Public, internal, webhook, admin, background-triggered, generated, and third-party-facing endpoints.
- `docs/api_map.md` when present as a discovery aid, then verify against current source.

## Issue classes

Look for concrete, reachable issues in:

- Method semantics, status codes, redirects, cache headers, CORS/CSRF assumptions, and content negotiation.
- Authn/authz behavior, tenant scoping, role/action checks, and status-code information leaks.
- Request validation, coercion, unknown fields, file/upload boundaries, body/query/path param consistency, and schema enforcement.
- Error envelope consistency, operator/user-safe diagnostics, partial success, and retry semantics.
- Response shape stability: field names, nullability, enum values, timestamps, serialization, sorting, and localization-sensitive values.
- Pagination, filtering, sorting, cursor stability, idempotency, async operation status, rate limits, quota headers, and webhooks.
- Versioning, deprecation, generated schema/client drift, and docs that would mislead consumers.
- REST/GraphQL/RPC conventions where the repository already relies on them.

## Priority model

### P0

Consumer-breaking contract bug, auth/security leak, tenant isolation issue, data corruption, missing validation in sensitive path, unsafe status semantics, payment/webhook/idempotency failure.

### P1

Reachable inconsistency causing client confusion, partial failures, duplicated API/domain logic, shallow critical coverage, pagination/filtering drift, or operational ambiguity.

### P2

Lower-risk contract hygiene with clear consumer impact: misleading docs, minor envelope drift, weak deprecation handling, unclear optionality, or localized inconsistency.

## Work item quality

- Output findings as compact chat work items; do not assume a platform-specific task workflow or extra delegation mechanism.
- Each work item must cite `path:line[-line]` evidence for the problematic behavior/contract and the owner layer, plus symbol when possible.
- Include reachable surface, affected actors/consumers/states, expected behavior, acceptance criteria, and validation direction when discoverable.
- Use one unambiguous fix direction per work item; no alternatives.
- Merge symptoms under the same behavior owner/source of truth unless fixes, rollout units, or validation differ.
- Do not report theoretical risks, stylistic preferences, or generic best practices without current repo impact.
- Do not report generic REST purity issues unless the inconsistency creates current consumer or system impact.

## Output contract

Produce chat work items grouped by P0/P1/P2. If none qualify, output each priority with `None`. Use compact chat bullets; do not force a rigid work-item schema.
