# Task Shaping

## Mode

- Use the active `CLAUDE.md` context if present, then repository evidence.
- Work in the current Claude Code Cloud session. Do not assume hidden background runs or extra delegation mechanisms unless the user explicitly provides them.
- Analysis-only mode: inspect the repository, do not edit code, and do not prepare a patch.

## Goal

Turn the user request into exactly one implementation-ready chat prompt for this repository.

## Inspect

- User intent and the concrete behavior change or behavior problem.
- Owner layer / source of truth for that behavior.
- Main affected modules, files, symbols, routes, commands, schemas, tests, docs, or generated artifacts.
- Reachable surface that matters for this task, including direct consumers and user/system states.

## Shaping rules

- Ground the task in current repository evidence with `path:line[-line]` anchors plus symbol when possible.
- Distinguish direct repository facts from assumptions or inference.
- Make the task atomic enough for one Claude Code implementation pass / one PR, but complete enough to solve the behavior across directly affected surfaces.
- Include problem/change, owner/source of truth, affected surface, expected result, acceptance criteria, validation, and out-of-scope boundaries in the chat prompt.
- Preserve existing contracts and unrelated behavior unless the requested change explicitly requires a contract change.
- For user-facing work, include relevant UX/UI/copy expectations and affected states.
- For API/integration work, include contract, validation, error, idempotency, versioning, and consumer impact when relevant.
- For new functionality, extend existing seams and patterns before introducing a new boundary.
- If the request bundles independent fixes, shape only the primary repo-supported fix and mark nearby work as out of scope inside the chat prompt.
- Ask exactly one clarifying question only when proceeding would be unsafe or would require a missing business/contract decision that the repo cannot resolve.

## Output contract

Output exactly one chat-ready implementation prompt. Do not edit files and do not create a platform-specific task object.

______________________________________
