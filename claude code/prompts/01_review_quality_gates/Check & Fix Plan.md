# Check & Fix Plan

## Mode

- Use the active `CLAUDE.md` context if present, then repository evidence.
- Work in the current Claude Code Cloud session. Do not assume hidden background runs or extra delegation mechanisms unless the user explicitly provides them.
- Analysis-only mode: inspect the repository, do not edit product code.

## Goal

Run a deep static/semantic/intent audit of repository behavior and produce unambiguous remediation work items. Every kept issue must answer: “What concrete system behavior problem does this fix?”

## Inspect

Business/domain logic, invariants, API/UI/DB sync, routes, handlers, services, state stores, jobs, migrations, configs, tests, CI, docs, generated artifacts, and user-visible flows. Follow references from the owner layer outward to affected consumers.

## Priority model

### P0 — high impact

- Business/domain logic defects, broken invariants, wrong conditions, invalid states.
- Regressions, public/internal contract violations, data corruption, lost updates, races/deadlocks, inconsistent transactional boundaries.
- Security, permission, tenant, payment, migration, or destructive-action behavior defects with concrete reachability.

### P1 — medium impact

- Duplicated domain logic that can diverge.
- Architecture violations with behavioral impact.
- Missing error handling in critical flows, partial-success ambiguity, state desynchronization across UI/API/DB.
- Hot-path performance affecting UX, cost, reliability, or operational clarity.
- Important workflow/test gaps that can realistically allow regression.

### P2 — lower but actionable impact

- Leaky abstractions or tight coupling that materially blocks safe change.
- Dead or misleading code in core logic.
- Config/flag complexity that makes behavior contradictory or non-obvious.
- Minor but real contract/UX inconsistencies with reachable impact.

## Finding rules

- Create work items only for concrete reachable behavior problems, contract exposure, observable inconsistency, or repo-proven regression risk.
- Each work item must cite `path:line[-line]` evidence for the problematic behavior/contract and owner layer, plus symbol when possible.
- Include affected surface, current impact, authoritative fix direction, acceptance criteria, and validation direction.
- Use one authoritative fix direction per work item; no alternatives.
- Collapse symptoms that share the same behavior owner and authoritative fix unless separate rollout units are clearly required.
- Do not report theoretical risks, style-only cleanup, generic hardening, or broad “best practice” changes without current repo impact.
- Prefer a complete high-value queue over one tiny fix. Stop when remaining findings are weak, duplicative, or outside the requested audit scope.
- Cap at 10 work items per priority; include the highest-impact issues with the strongest evidence.

## Output contract

Produce chat work items grouped by P0/P1/P2. If no qualifying issues are found, output each priority with `None`. Use compact chat bullets; do not force a rigid markdown schema.
