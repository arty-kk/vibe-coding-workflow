# Migration & Refactor

## Mode

- Use the active `AGENTS.md` chain.
- Execute mode: change the repository when changes are justified by current evidence.

## Goal

Execute one coherent migration/refactor slice that improves structure, ownership, API usage, or maintainability while preserving current behavior unless the user explicitly requested a behavior change.

## Scope selection

- Use the user’s named migration/refactor target when provided.
- If the request is broad, identify the strongest owner-layer improvement with clear reachable benefit and limited risk.
- Include directly affected call sites, tests, docs, generated artifacts, and configuration.
- Avoid unrelated cleanup, speculative abstractions, new dependencies, and multi-track rewrites.

## Refactor targets

- Duplicated source-of-truth logic that can diverge.
- Layering violations that make behavior or contracts hard to enforce.
- Deprecated API/library usage with clear repo-visible replacement path.
- Naming/ownership/call-site drift that blocks safe change.
- Type/schema/model boundaries that should move together.
- Dead replaced paths when compatibility no longer requires them.

## Implementation principles

- Start from owner implementation and follow usages outward.
- Preserve public/internal contracts unless the task explicitly changes them.
- Prefer one coherent seam over scattered local edits.
- Keep migration reversible or easy to review; update tests and docs where the repo uses them.
- Do not hide behavior changes under a refactor label.

## Validation

Run relevant repository-native checks. When explaining non-obvious repo facts, skipped adjacent work, or detected behavior, cite `path:line[-line]` where useful.

Compare affected before/after behavior through tests or static call-site review.

## Final response

Respond in Russian with compact emoji sections: ♻️ changed surfaces, 📁 key files, 🧪 checks, 👀 manual review/trace, ⚠️ assumptions/risks, ⛔ not run/not included.
