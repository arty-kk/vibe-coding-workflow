# Notification Surface Audit

## Mode

- Use the active `CLAUDE.md` context if present, then repository evidence.
- Work in the current Claude Code Cloud session. Do not assume hidden background runs or extra delegation mechanisms unless the user explicitly provides them.
- Analysis-only mode: inspect the repository, do not edit product code.

## Goal

Audit user-facing notification behavior across transactional emails, in-app notifications, push/SMS/webhooks when present, toasts, banners, reminders, and system alerts. Keep only issues with repository evidence and reachable user or operator impact.

## Inspect

Email/templates, notification services, event producers, queues/jobs, delivery providers/adapters, preference/unsubscribe logic, i18n catalogs, auth/tenant context, user roles, billing/security/product flows, retry/debounce/idempotency logic, logs/metrics, tests, docs, and preview tooling.

## Issue classes

Look for concrete, reachable issues in:

- Trigger correctness: notifications sent too early/late, duplicated, missing on important outcome, sent to wrong role/tenant, or not idempotent on retries.
- Content and state: subject/body/CTA/preview text inconsistent with product state, missing failure/recovery copy, unsafe diagnostics, broken links, stale branding, or unsupported claims.
- Preferences and compliance-adjacent behavior: unsubscribe/preferences ignored where repo models them, transactional vs marketing confusion, locale mismatch, or privacy-sensitive payloads.
- Delivery and operations: queue/retry gaps, provider errors not surfaced safely, no template previews/tests, broken variables/interpolation, missing observability.
- Regression resistance: no tests/fixtures for important templates, stale docs, or notification ownership spread across producers.

## Priority model

### P0

Notification can leak data across tenants/users, trigger destructive or billing/security confusion, expose secrets/PII, or repeatedly spam users due to retry/idempotency bugs.

### P1

Important notification missing/wrong/duplicated, broken recovery link, misleading lifecycle content, ignored preferences where modeled, or missing tests on high-value templates.

### P2

Lower-risk but concrete quality issue: weak copy, stale subject, missing preview, minor locale drift, secondary event gap, or maintainability issue in notification ownership.

## Work item quality

- Output findings as compact chat work items; do not assume a platform-specific task workflow or extra delegation mechanism.
- Each work item must cite `path:line[-line]` evidence for the trigger/template owner and affected recipient/state.
- Include expected trigger, recipient, content/state, acceptance criteria, and validation direction.
- Merge issues by notification owner when one fix validates them together.

## Output contract

Produce chat work items grouped by P0/P1/P2. If none qualify, output each priority with `None`. Use compact chat bullets; do not force a rigid work-item schema.
