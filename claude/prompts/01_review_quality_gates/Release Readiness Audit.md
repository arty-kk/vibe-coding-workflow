# Release Readiness Audit

## Mode

- Use the active `CLAUDE.md` context if present, then repository evidence.
- Work in the current Claude Code Cloud session. Do not assume hidden background runs or extra delegation mechanisms unless the user explicitly provides them.
- Analysis-only mode: inspect the repository, do not edit product code.

## Goal

Audit whether a repository or selected feature is ready to ship: correctness, tests, migrations, config, deploy path, observability, security/privacy, UI states, docs, and rollback/recovery. Keep only issues supported by repository evidence and relevant to release risk.

## Inspect

Changed or selected feature areas, routes/API/jobs/workers, migrations/schemas, env/config, CI/deploy files, tests, feature flags, seed data, docs/runbooks, logs/metrics/health checks, user-facing copy/states, security/privacy boundaries, package/lockfiles, and recent generated maps/plans if present.

## Issue classes

Look for concrete, reachable release blockers or risks in:

- Contract readiness: API/UI/job/schema drift, migration ordering, generated artifact mismatch, missing env/config, version/dependency drift, or external integration mismatch.
- Validation readiness: missing owner-level tests for changed behavior, brittle snapshots, unrun critical checks, no seed/fixture for release path, or visual/regression gaps on main surfaces.
- Operational readiness: missing health/logging/metrics for new failure path, deploy/rollback ambiguity, unsafe cleanup, background job ordering, or absent runbook for critical change.
- Product readiness: missing loading/error/empty/no-access/no-plan/destructive states, misleading copy, unsupported public claims, broken onboarding/billing/permission edge.
- Security/privacy readiness: secret/PII leakage, missing authorization enforcement, unsafe diagnostics, tenant isolation risk, or compliance-sensitive data retention/config issue.

## Priority model

### P0

Release can cause data loss/corruption, security/privacy breach, broken paid/core workflow, failed deploy/migration, or irreversible user harm.

### P1

Meaningful release risk: missing tests/checks for high-impact behavior, operational blind spot, important UI state gap, integration drift, or rollback/recovery uncertainty.

### P2

Lower-risk but concrete readiness issue: stale docs/runbook, minor config ambiguity, secondary test gap, weak copy/state, or maintainability issue likely to slow release support.

## Work item quality

- Output findings as compact chat work items; do not assume a platform-specific task workflow or extra delegation mechanism.
- Each work item must cite `path:line[-line]` evidence for the release risk and affected owner.
- Include expected release-safe behavior, acceptance criteria, validation direction, and whether it blocks release or can follow after release.
- Merge issues by release owner/source of truth when one fix validates them together.

## Output contract

Produce only chat work items grouped by P0/P1/P2, with a one-line release verdict: `ship`, `ship with known P2s`, `hold for P1/P0`, or `insufficient evidence`. If none qualify, output each priority with `None`.
