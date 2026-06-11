# Onboarding Activation Audit

## Mode

- Use the active `AGENTS.md` chain.
- Plan mode only: inspect the repository, do not edit product code.

## Goal

Audit the path from first entry to meaningful activation: public entry, signup/login, first-run state, workspace/project setup, permissions, plan gates, sample data, checklist/progress, handoff into core workflow, and activation measurement. Keep only issues supported by repository evidence.

## Inspect

Public routes, auth flows, onboarding routes/components, empty states, setup wizards, workspace/project/team creation, invitations, plan/trial/quota gates, seed/demo/sample data, emails/notifications, analytics events, feature flags, docs, tests, and navigation maps.

## Issue classes

Look for concrete, reachable issues in:

- Entry-to-value continuity: unclear next step, dead ends after signup/login, missing first-run state, inconsistent redirect, setup steps not aligned with core workflow.
- Setup correctness: workspace/project/team/role/plan context not established, sample data conflicts with permissions, incomplete defaults, or invalid states after partial setup.
- Activation clarity: checklist/progress/CTA copy does not match implemented behavior, success state lacks next step, upgrade/trial/no-access states block without explanation.
- Recovery: failed invite/payment/setup/import/integration states lose user input or do not provide a safe retry path.
- Measurement: activation-critical events missing, duplicated, fired before success, leaking PII, or impossible to connect to funnel state using existing instrumentation patterns.
- Regression resistance: no tests/previews for primary first-run path, stale docs, or route guards that make onboarding fragile.

## Priority model

### P0

Signup/onboarding path creates broken tenant/auth/plan state, loses data, blocks paid/core activation, or exposes data across tenants/roles.

### P1

Important first-run friction, missing setup state, misleading plan/trial guidance, broken recovery, or measurement gap that prevents validating activation.

### P2

Lower-risk but concrete activation improvement: weak empty-state copy, stale checklist/docs, minor redirect inconsistency, or missing test for a secondary onboarding state.

## Task-sub quality

- Use native Codex Cloud task-sub creation when available; do not force a handmade markdown task-sub body.
- Every task-sub must cite `path:line[-line]` evidence for route/state owner and affected activation step.
- Include affected role/plan/tenant state, expected behavior, acceptance criteria, and validation direction.
- Merge symptoms that share the same onboarding owner/source of truth.

## Output contract

Produce only native Codex Cloud task-subs grouped by P0/P1/P2. If none qualify, output each priority with `None`. Do not print a custom task-sub schema.
