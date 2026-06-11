# Task Shaping

## Mode

- Use the active `AGENTS.md` chain.
- Plan mode only: inspect the repository, do not edit code, and do not prepare a patch.

## Goal

Turn the user request into exactly one implementation-ready native Codex Cloud task-sub for this repository.

## Inspect

- User intent and the concrete behavior change or behavior problem.
- Owner layer / source of truth for that behavior.
- Main affected modules, files, symbols, routes, commands, schemas, tests, docs, or generated artifacts.
- Reachable surface that matters for this task, including direct consumers and user/system states.

## Shaping rules

- Ground the task in current repository evidence with `path:line[-line]` anchors plus symbol when possible.
- Distinguish direct repository facts from assumptions or inference.
- Make the task atomic enough for one execute run / one PR, but complete enough to solve the behavior across directly affected surfaces.
- Include problem/change, owner/source of truth, affected surface, expected result, acceptance criteria, validation, and out-of-scope boundaries in the native task-sub content.
- Preserve existing contracts and unrelated behavior unless the requested change explicitly requires a contract change.
- For user-facing work, include relevant UX/UI/copy expectations and affected states.
- For API/integration work, include contract, validation, error, idempotency, versioning, and consumer impact when relevant.
- For new functionality, extend existing seams and patterns before introducing a new boundary.
- If the request bundles independent fixes, shape only the primary repo-supported fix and mark nearby work as out of scope inside the native task-sub.
- Ask exactly one clarifying question only when proceeding would be unsafe or would require a missing business/contract decision that the repo cannot resolve.

## Output contract

Create the task-sub through Codex Cloud’s native task-sub flow. Do not print a custom markdown task-sub template in chat unless the native mechanism is unavailable.

______________________________________
