# Consistency Invariants Audit

## Mode

- Use the active `CLAUDE.md` context if present, then repository evidence.
- Work in the current Claude Code Cloud session. Do not assume hidden background runs or extra delegation mechanisms unless the user explicitly provides them.
- Analysis-only mode: inspect the repository, do not edit product code.

## Goal

Find reachable consistency defects where one business rule, state transition, permission, quota, schema, cache, generated type, or external contract can drift across layers or over time.

## Relation to existing prompts

Use this prompt for cross-layer invariant drift where the owner/source of truth is unclear or spans API, storage, UI, caches, jobs, generated artifacts, and docs. If the domain is specifically auth/tenant/role behavior, use `09_business_rules_data_analytics/Auth Permissions Audit.md`. If the domain is plans, quotas, subscriptions, billing providers, or entitlement gates, use `09_business_rules_data_analytics/Billing Entitlements Audit.md`. If the concern is mainly schema/model shape and migrations, use `09_business_rules_data_analytics/Data Model Audit.md`.

## Inspect

Domain models, validators, permissions, plan/quota rules, API schemas, database constraints, migrations, generated clients/types, UI state gates, caches, background jobs, integrations, tests, fixtures, docs, and analytics/event contracts.

## Focus areas

- Duplicate sources of truth for rules, states, enums, permissions, quotas, feature flags, copy, cache keys, external payloads, or validation.
- State-machine gaps: invalid transitions, impossible states representable in storage/types/UI, missing terminal states, or ambiguous rollback/compensation behavior.
- Read/write drift: UI accepts states the API rejects, API accepts states storage cannot enforce, generated clients differ from handlers, or docs disagree with runtime contracts.
- Cache/search/index drift: invalidation gaps, stale denormalized fields, async projection races, missing repair/rebuild path, or inconsistent pagination/sorting semantics.
- Tenant/workspace/project isolation drift between route params, auth context, filters, policies, analytics, and background jobs.
- Test/doc drift where guard tests, fixtures, examples, or README instructions encode a contract different from the implementation owner.

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

- Output findings as compact chat work items; do not assume a platform-specific task workflow or extra delegation mechanism.
- Every work item must include affected surface, actors/consumers/states, expected behavior, acceptance criteria, and validation direction when discoverable.
- Use one unambiguous fix direction per work item; no alternatives.
- If validation commands or harnesses are absent, specify observable checks that an implementation pass can add or perform.

## Output contract

Respond in Russian with grouped P0/P1/P2 chat work items. If none qualify, write `None` for that priority. Keep each item compact but evidence-backed.
