# Validation & Clarification

## Mode

- Use the active `AGENTS.md` chain.
- Plan mode only: validate exactly one incoming task-sub or short task statement.
- Do not edit code or prepare a patch.

## Goal

Decide whether the task is relevant, necessary, correctly scoped, and safe to execute as one Codex Cloud task. If valid, recreate exactly one implementation-ready native task-sub. If invalid, block it with evidence.

## Validation pass

1. Identify intended behavior change, affected surface, owner layer, expected outcome, and likely validation.
2. Verify against current repository evidence whether:
   - the issue or need exists now;
   - it is already solved fully or partially elsewhere;
   - it conflicts with architecture, conventions, contracts, style, or `AGENTS.md`;
   - affected components, modules, tests, configs, docs, migrations, generated artifacts, or consumers are discoverable;
   - the task is the right size for one execute run / one PR.
3. Cite `path:line[-line]` or nearest stable locator such as `path#symbol` for every verdict.
4. Separate direct evidence from inference. Never present inference as repository fact.
5. Do not turn weak hypotheses, taste preferences, speculative hardening, or generic cleanup into a task-sub without evidence of current impact, concrete risk, or missing required behavior.
6. If the task bundles independent fixes, keep only the primary repo-proven fix in the recreated task-sub and put nearby work out of scope. If no safe primary fix exists, request clarification.
7. Ask exactly one clarifying question only when a missing product/business/contract decision prevents safe execution and repository evidence cannot resolve it.

## Verdict handling

- If the task is not needed, already solved, unsupported by repo evidence, incorrectly formulated, or aimed at the wrong owner layer, start with `⚠️ Task is not relevant:` and give a short reason with `path:line[-line]` evidence.
- If the task is relevant, recreate exactly one native Codex Cloud task-sub with unambiguous scope, expected result, evidence, acceptance criteria, and validation.

_______________________________
