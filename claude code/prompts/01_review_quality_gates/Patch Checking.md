# Patch Checking

## Mode

- Use the active `CLAUDE.md` context before identifying the patch baseline or running checks.
- Work in the current Claude Code Cloud session. Do not assume hidden background runs or extra delegation mechanisms unless the user explicitly provides them.
- Post-implementation review mode: review the full detected patch range, validate it against repo-visible reachable contracts, and edit only to fix issues introduced by, required by, or directly exposed by that range.

## Goal

Confirm that the prepared patch is correct, scoped, and compatible with existing behavior. If defects are found, apply the single best fix per defect. If no defects are found, report a clean verdict with checked scope, evidence, and validation status.

## Domain anti-patterns

- Do not report style preferences, theoretical risks, or generic best practices without repo-visible reachability and impact.
- Do not ignore producer/consumer contracts outside the local diff when the changed symbol is shared.
- Do not review only the latest commit when the patch spans multiple commits; establish the full branch/diff range first.
- Do not treat skipped checks, absent benchmarks, or missing fixtures as confidence.
- Do not propose broad rewrites, dependency upgrades, or architecture migrations as quality-gate fixes unless the current defect requires them.
- Do not split one root cause into multiple work items or merge unrelated defects that need different owners or validation paths.

## Patch range and baseline

Review the complete patch range, not just the latest commit.

Identify the review target in this order:

1. Explicit user-provided diff, PR target, branch, commit range, or single commit.
2. Otherwise the current branch delta against its PR target, upstream, tracking branch, or repo default branch when visible.
3. Otherwise the current working tree, staged diff, and untracked files.

If no patch range, diff, branch delta, staged/unstaged change, or untracked file can be identified, output exactly: `Patch not found: no changed files or review target visible.`

Then stop.

## Review scope

1. Inventory changed files, changed symbols, commits in scope, and affected behavior surfaces from the full patch range.
2. Reconstruct the full contract of every changed behavior, symbol, API, schema, state transition, configuration key, or data shape.
3. Read the complete execution path around the change:
   - upstream callers;
   - downstream consumers;
   - sibling implementations of the same contract;
   - interfaces, abstractions, and adapters;
   - persistence, transport, cache, queue, and serialization boundaries when touched.
4. Search all repo-visible usages, call sites, implementations, overrides, exports/imports, tests, fixtures, configs, docs, migrations, generated artifacts, and consumers of changed contracts.
5. Do not stop at the modified files. Continue expanding the review until all affected contracts have at least one validated producer path and one validated consumer path.
6. Check for:
   - logic errors and edge-case regressions;
   - API/data/schema/type contract mismatches;
   - auth/session/role/tenant/plan behavior drift when relevant;
   - incorrect loading/empty/error/disabled/no-access/user-visible states when relevant;
   - races, locks, transactions, idempotency, or consistency risks when relevant;
   - backwards-compatibility breaks for existing callers/consumers;
   - test, fixture, doc, config, migration, generated artifact, or deploy drift caused by the patch;
   - contract incompleteness: changed behavior validated only locally but not across all reachable producers and consumers;
   - partial updates where one implementation of a shared contract changed but peer implementations did not;
   - assumptions that are no longer true for existing callers;
   - repo-visible style, lint, type, or convention violations.

## Evidence rules

- Every concern must cite direct repository evidence as `path:line[-line]` plus nearest symbol when possible.
- Separate direct evidence from inference. Never present inference as repository fact.
- Do not expand scope. Unrelated issues found during review become follow-up work items, not patch-check fixes.

## Fix rules

- Fix only concrete problems in the prepared patch.
- Prefer the behavior owner / authoritative layer over local workarounds.
- Use one best-practice fix per issue; do not propose alternatives.
- Update or add tests only when the patch changes tested behavior or the repo clearly has the relevant test harness.
- Keep patch-check edits isolated. If the repo/cloud workflow supports commits and a commit is expected, create a separate patch-check commit; otherwise leave edits in the current diff and report that no separate commit was created.
- Do not introduce new dependencies, migrations, public contracts, or broad refactors unless required to make the current patch correct.

## Contract coverage gate

Before declaring the patch clean, identify:

- changed contracts;
- producers of each contract;
- consumers of each contract.

A patch cannot receive a clean verdict if any changed contract has unreviewed reachable producers or consumers inside the repository.

## Validation

Run repo-native checks discoverable from `CLAUDE.md`, package scripts, Makefile, CI config, or docs and relevant to the changed surface. Do not invent commands. If a relevant check cannot run, report why.

## Output style

For a clean patch, start exactly with `✅ Everything is fine. No changes required 👌`. Then keep the response concise with native status sections: 👀 checked scope, 🔎 evidence, 🧪 validation, ⚠️ assumptions/risks if any.

For a fixed patch, start with `🛠️ Patch-check fixes applied`. Then summarize ✅ fixed issues, ♻️ changed files, 🔎 evidence, 🧪 validation, and ⚠️ remaining risks. Avoid rigid placeholder templates.
