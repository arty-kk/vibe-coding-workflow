# Bot Audit

## Mode

- Use the active `AGENTS.md` chain.
- Plan mode only: inspect the repository, do not edit product code.

## Goal

Audit bot flows, commands, state transitions, keyboards, copy, permissions, and platform constraints. Keep issues that affect user completion, safety, correctness, or operability.

## Inspect

Commands, message/callback handlers, routers, scenes/FSM states, keyboards, templates/copy, middleware, auth/permissions, deep links, scheduled/proactive messages, external integrations, persistence, i18n, tests, docs, and generated bot navigation maps.

## Issue classes

Look for concrete, reachable issues in:

- Entry points: `/start`, `/help`, command list, deep links, onboarding, restart/recovery.
- Navigation/state: back/home/cancel, stale callbacks, invalid state recovery, unreachable states, cyclic dead ends, concurrent messages, session expiry.
- Keyboards/buttons: labels, ordering, destructive confirmation, callback payload limits, duplicate actions, platform-specific behavior.
- Input handling: accepted formats, validation, retry copy, free-text safety, attachment handling, rate/abuse controls.
- Permissions/privacy: admin/staff commands, user identity, group/private chat behavior, tenant/account context, sensitive data exposure.
- Message quality: formatting/escaping, length limits, localization, safe errors, empty/unavailable states, async/proactive status updates.
- Integration and persistence: payment/external callbacks, idempotency, duplicate deliveries, job scheduling, DB state sync, telemetry where present.

## Priority model

### P0

Security/privacy leak, permission bypass, payment/webhook/idempotency bug, state-machine dead end in a critical flow, destructive action risk, or data consistency issue.

### P1

Important flow cannot be completed reliably, stale callback/retry/error handling gap, unclear validation in core flow, duplicate flow logic, or missing critical bot coverage.

### P2

Lower-risk but concrete navigation/copy/state/accessibility issue that affects comprehension, support load, or safe future change.

## Task-sub quality

- Use native Codex Cloud task-sub creation when available; do not force a handmade markdown task-sub body.
- Every task-sub must cite `path:line[-line]` evidence for the problematic behavior/contract and the owner layer, plus symbol when possible.
- Include reachable surface, affected actors/consumers/states, expected behavior, acceptance criteria, and validation direction when discoverable.
- Use one unambiguous fix direction per task-sub; no alternatives.
- Merge symptoms under the same behavior owner/source of truth unless fixes, rollout units, or validation differ.
- Do not report theoretical risks, stylistic preferences, or generic best practices without current repo impact.
- Include affected user role, chat type, state, command, or callback when relevant.
- Do not create tasks for platform features the repo does not currently use or expose.

## Output contract

Produce only native Codex Cloud task-subs grouped by P0/P1/P2. If none qualify, output each priority with `None`. Do not print a custom task-sub schema.
