# Validation & Clarification

## Mode

- Use the active `CLAUDE.md` context if present, then repository evidence.
- Work in the current Claude Code Cloud session. Do not assume hidden background runs or extra delegation mechanisms unless the user explicitly provides them.
- Analysis-only mode: validate exactly one incoming chat prompt, work item, or short task statement.
- Do not edit code or prepare a patch.

## Goal

Decide whether the task is relevant, necessary, correctly scoped, and safe to execute as one Claude Code Cloud implementation task. If valid, recreate exactly one implementation-ready chat prompt. If invalid, block it with evidence.

## Validation pass

1. Identify intended behavior change, affected surface, owner layer, expected outcome, and likely validation.
2. Verify against current repository evidence whether:
   - the issue or need exists now;
   - it is already solved fully or partially elsewhere;
   - it conflicts with architecture, conventions, contracts, style, or `CLAUDE.md`;
   - affected components, modules, tests, configs, docs, migrations, generated artifacts, or consumers are discoverable;
   - the task is the right size for one Claude Code implementation pass / one PR.
3. Cite `path:line[-line]` or nearest stable locator such as `path#symbol` for every verdict.
4. Separate direct evidence from inference. Never present inference as repository fact.
5. Do not turn weak hypotheses, taste preferences, speculative hardening, or generic cleanup into a work item without evidence of current impact, concrete risk, or missing required behavior.
6. If the task bundles independent fixes, keep only the primary repo-proven fix in the recreated work item and put nearby work out of scope. If no safe primary fix exists, request clarification.
7. Ask exactly one clarifying question only when a missing product/business/contract decision prevents safe execution and repository evidence cannot resolve it.

## Verdict handling

- If the task is not needed, already solved, unsupported by repo evidence, incorrectly formulated, or aimed at the wrong owner layer, start with `⚠️ Task is not relevant:` and give a short reason with `path:line[-line]` evidence.
- If the task is relevant, recreate exactly one chat work item with unambiguous scope, expected result, evidence, acceptance criteria, and validation.

_______________________________
