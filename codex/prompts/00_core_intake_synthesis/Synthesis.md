# Synthesis

## Mode

- Use the active `AGENTS.md` chain.
- Plan mode only: reconcile audit outputs and repository evidence, do not edit product code.

## Goal

Merge two or more audit outputs into a deduplicated, prioritized batch of native Codex Cloud task-subs. Preserve the strongest repository evidence as exact `path:line[-line]` anchors and remove duplicates, conflicts, weak findings, and non-actionable recommendations.

## Inputs

Use available outputs from this workflow, especially:

- `Check & Fix Plan.md`
- `Security Audit.md`
- `API Audit.md`
- `SaaS Audit.md`
- `Bot Audit.md`
- `Test Coverage Audit.md`
- `Performance Audit.md`
- `Evolution & Improvement.md`

Generated maps, docs, and old audit outputs are hints. When an input lacks `path:line[-line]` evidence or looks stale, verify the relevant repository files before keeping the task.

## Reconciliation rules

- Merge findings that share the same behavior owner and authoritative fix, even if they came from different audits.
- Keep separate tasks when fixes belong to different owners, rollout units, validation strategies, roles, plans, tenants, or contracts.
- Re-rank by actual impact using repository evidence, not by the source audit’s label.
- Every kept task-sub must retain exact `path:line[-line]` anchors plus symbol when possible.
- Preserve dependencies when one task enables another; do not hide a dependent task if both remain useful.
- Drop tasks that are already solved, speculative, cosmetic without impact, duplicated, stale, or based only on generated maps.
- Surface unresolved conflicts only when sources disagree on facts, scope, or fix direction and repository evidence does not resolve it.
- Prefer a complete high-value queue over a tiny set of obvious fixes; stop when remaining findings are weak or duplicative.

## Output contract

Produce only native Codex Cloud task-subs grouped by P0/P1/P2. Each task-sub must preserve concrete evidence anchors, source references, dependency notes when relevant, and one unambiguous implementation direction. If no tasks remain, output each priority with `None`. Do not print a custom task-sub schema.
