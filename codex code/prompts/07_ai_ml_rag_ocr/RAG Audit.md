# RAG Audit

## Mode

- Use the active `AGENTS.md` chain.
- Plan mode only: inspect the repository, do not edit product code.

## Goal

Audit retrieval-augmented generation behavior from ingestion to answer rendering. Keep only reachable issues that affect answer correctness, source grounding, access control, freshness, latency/cost, or regression resistance.

## Inspect

Document loaders, parsers, chunkers, metadata extraction, embeddings, vector/search indexes, hybrid search, rerankers, query rewriting, filters/ACL checks, tenant scoping, deletion/reindex flows, answer prompts, citation/source rendering, cache/freshness logic, admin ingestion UI, queues/jobs, tests/evals, telemetry, docs, and `docs/ai_map.md` when present.

## Issue classes

Look for concrete, reachable issues in:

- Ingestion and indexing: stale or missing reindex paths, duplicate chunks, unstable IDs, broken deletion, bad file-type handling, lost metadata, and unbounded document size.
- Chunking and retrieval quality: chunk boundaries that drop critical context, missing title/section metadata, no multilingual handling where repo serves multiple locales, weak top-k/rerank defaults with current impact, and query rewrite drift.
- Access control: tenant/user/project ACL not applied consistently at ingestion, search, rerank, cache, or answer rendering.
- Grounding and citations: generated answers cite missing/wrong sources, source snippets cannot support claims, UI hides uncertainty, or answer prompt allows unsupported claims.
- Freshness and consistency: source docs change without invalidating index/cache, background jobs silently fail, partial ingestion is presented as complete, or embeddings/index schema drift from retrieval code.
- Operational behavior: high-cost retrieval loops, rate-limit gaps, slow hot paths, missing telemetry for empty/low-confidence retrieval, and absent operator recovery paths.
- Evaluation: missing eval fixtures for representative queries, ACL filtering, citation correctness, stale-index behavior, or known answer regressions.

## Priority model

### P0

Cross-tenant/source leakage, unauthorized retrieval, answer path that can trigger destructive/paid/security decisions from unsupported context, broken critical answer flow, or stale/deleted content exposed as current.

### P1

Important retrieval/citation/freshness defect with user-visible impact, missing critical RAG eval, duplicated retrieval/domain logic, unbounded cost/latency on reachable use, or ingestion state that misleads users/operators.

### P2

Lower-risk but concrete RAG quality issue: weak metadata, unclear empty/low-confidence state, stale docs/map, minor eval gap, or source UI ambiguity that affects trust.

## Task-sub quality

- Use native Codex Cloud task-sub creation when available; do not force a handmade markdown task-sub body.
- Every task-sub must cite `path:line[-line]` evidence for the ingestion/retrieval/answer owner and affected surface, plus symbol when possible.
- Include data source, index/retriever owner, ACL/freshness boundary, expected behavior, acceptance criteria, and validation/eval direction when discoverable.
- Use one unambiguous fix direction per task-sub; no alternatives.
- Merge symptoms under the same retrieval owner unless fixes, rollout units, index migration, or eval strategy differ.
- Do not recommend provider/model/vector database swaps unless current repo evidence proves the existing owner cannot satisfy the behavior.

## Output contract

Produce only native Codex Cloud task-subs grouped by P0/P1/P2. If none qualify, output each priority with `None`. Do not print a custom task-sub schema.
