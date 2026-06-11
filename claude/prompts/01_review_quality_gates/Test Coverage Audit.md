# Test Coverage Audit

## Mode

- Use the active `CLAUDE.md` context if present, then repository evidence.
- Work in the current Claude Code Cloud session. Do not assume hidden background runs or extra delegation mechanisms unless the user explicitly provides them.
- Analysis-only mode: inspect the repository, do not edit product code.

## Goal

Find critical behavior that is untested, falsely tested, or fragile enough to allow regressions. Keep coverage gaps that matter to correctness, contracts, security, UX, or operability.

## Inspect

Tests, test utilities, fixtures, mocks, snapshots, coverage config, CI workflows, package scripts, and the source behavior those tests claim to protect. Include generated maps/docs only as discovery aids.

## Coverage issues

Look for concrete, reachable issues in:

- Missing tests for reachable critical behavior.
- Tests that assert implementation details while missing observable behavior.
- Mocks/stubs that bypass the risk being tested.
- Snapshot-only or smoke-only coverage for behavior with branching rules.
- Flaky-risk patterns: real timers/network, order coupling, shared mutable state, nondeterministic data, unawaited async work.
- CI not running the tests that protect important behavior.
- Tests or fixtures that encode outdated contracts and would hide regressions.

## Priority model

### P0

Missing or false coverage for security, data integrity, payment, tenant isolation, destructive mutation, migration, or externally visible contract.

### P1

Missing meaningful coverage for important workflows, state transitions, error handling, integration boundaries, UI/API behavior, or hot paths likely to regress.

### P2

Lower-risk but useful coverage improvement for misleading tests, flaky risk, weak assertions, or unverified edge states.

## Work item quality

- Output findings as compact chat work items; do not assume a platform-specific task workflow or extra delegation mechanism.
- Each work item must cite `path:line[-line]` evidence for the problematic behavior/contract and the owner layer, plus symbol when possible.
- Include reachable surface, affected actors/consumers/states, expected behavior, acceptance criteria, and validation direction when discoverable.
- Use one unambiguous fix direction per work item; no alternatives.
- Merge symptoms under the same behavior owner/source of truth unless fixes, rollout units, or validation differ.
- Do not report theoretical risks, stylistic preferences, or generic best practices without current repo impact.
- Cite both the behavior owner and the missing/weak test evidence.
- Make each work item about adding or repairing tests for one behavior owner and state the expected observable assertion.
- Do not create product-code change tasks unless the code is untestable because of a demonstrated behavior-boundary problem.

## Output contract

Produce chat work items grouped by P0/P1/P2. If none qualify, output each priority with `None`. Use compact chat bullets; do not force a rigid work-item schema.
