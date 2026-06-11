# Notification Email Polish — Transactional Messages, In-App Alerts, and Recovery

## Mode

- Use the active `CLAUDE.md` context if present, then repository evidence.
- Work in the current Claude Code Cloud session. Do not assume hidden background runs or extra delegation mechanisms unless the user explicitly provides them.
- Implementation mode: change the repository when a focused notification/email improvement is justified by current evidence.

## Goal

Improve one coherent notification surface so the right recipient gets the right message at the right product state, with truthful copy, safe links, preference-aware delivery where modeled, and regression resistance.

## Scope selection

- If the user named an email, template, notification, toast, reminder, recipient, trigger, or audit work item, polish that owner and directly affected producers/consumers.
- If the request is broad, inspect high-impact transactional/product notifications and choose the highest-confidence fix with trust, safety, completion, or support impact.
- Include related copy, i18n, trigger logic, tests, previews, docs, and instrumentation when they belong to the same notification problem.
- Avoid new providers, marketing campaign strategy, deliverability vendor work, and unrelated product-flow changes unless the selected issue requires them.

## Polish targets

- Trigger and recipient correctness: role, tenant/workspace/project, actor vs subject, timing, dedupe/idempotency, retry behavior, and lifecycle state.
- Content: subject, preview text, heading, body, CTA, fallback link, recovery instructions, support-safe diagnostics, legal/privacy-sensitive wording, and localization.
- Template robustness: variables, escaping, formatting, dark/plain text variants when present, responsive email constraints, and preview fixtures.
- Preferences and safety: unsubscribe/preference handling where repo-modeled, transactional vs marketing boundaries, PII minimization, and safe logging.
- Directly affected tests, snapshots/previews, docs, and observability hooks when the repo uses them.

## Implementation principles

- Reuse existing template components, notification services, i18n catalogs, queues/jobs, and test/preview patterns.
- Keep copy aligned with actual product state and permission/plan behavior.
- Prefer owner-level trigger/template fixes over local string edits in producers.
- Do not expose raw errors, internal IDs, secrets, or cross-tenant data to recipients.

## Validation

Run relevant repository-native checks. When possible, verify template rendering/preview and trace one trigger path. State any inability to send real email or verify provider delivery.

## Final response

Respond in Russian with compact emoji sections: ♻️ changed notification surface, 📁 key files, 🔎 evidence anchors, 🧪 checks, 👀 template/trigger trace, ⚠️ assumptions/risks, ⛔ not run/not included.
