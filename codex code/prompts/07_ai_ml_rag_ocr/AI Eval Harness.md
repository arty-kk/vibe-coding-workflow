# AI Eval Harness

## Mode

- Use the active `AGENTS.md` chain.
- Execute/documentation mode: add or improve one repository-native eval harness for an AI/RAG/OCR/ML behavior when current evidence justifies it.

## Goal

Create a small, maintainable eval loop that can catch meaningful regressions in one AI behavior. The result should be runnable from repository-native scripts without external secrets unless the repo already has a safe eval pattern for them.

## Scope selection

- If the user named a feature, prompt, retriever, OCR extraction, model output, or bug class, build the eval around that behavior.
- If the request is broad, inspect AI-visible surfaces and choose the highest-risk behavior with the clearest deterministic or semi-deterministic scoring path.
- Prefer a narrow high-signal eval over a large brittle benchmark.
- Do not change production AI behavior unless a minimal change is required to expose the behavior to tests/evals cleanly.

## Eval targets

- Structured outputs: schema validity, enum/nullability, required fields, refusal/empty output handling, and parser errors.
- RAG: retrieval recall/precision proxy, metadata/ACL filtering, citation/source consistency, answer groundedness checks where feasible.
- OCR/document AI: field/table/checkbox extraction, page ordering, confidence thresholds, correction workflows, export shape.
- Tool/function calls: allowed tool selection, argument shape, validation failures, idempotency, and unsafe action prevention.
- Product behavior: visible loading/error/result states, user-safe diagnostics, generated-content labeling, and regression fixtures for known incidents.

## Implementation principles

- Reuse existing test runner, fixtures, mocks, scripts, package manager, and CI conventions.
- Keep eval data small, reviewable, and safe to commit. Do not commit secrets, private documents, or unredacted PII.
- Prefer deterministic fixtures, fake model adapters, recorded safe responses, or local scoring functions when they test the contract sufficiently.
- For live-model evals, gate them behind explicit env/config and document that they are optional if the repo lacks a safe live eval pattern.
- Add clear pass/fail thresholds only when the metric is meaningful; otherwise report a reviewable score artifact.
- Document how to run the eval and what failure means.

## Validation

Run the new or updated eval command plus directly affected tests when available. If live-model or document fixtures are unavailable, run the deterministic part and state the gap.

## Final response

Respond in Russian with compact emoji sections: ✅ eval harness, 📁 files changed, 🔎 behavior/evidence anchors, 🧪 checks and scores, ⚠️ assumptions/risks, ⛔ not run/not included.
