# Form UX Polish — Data Entry, Validation, Submission, and Recovery

## Mode

- Use the active `CLAUDE.md` context if present, then repository evidence.
- Work in the current Claude Code Cloud session. Do not assume hidden background runs or extra delegation mechanisms unless the user explicitly provides them.
- Implementation mode: change the repository when a focused form/data-entry improvement is justified by current evidence.

## Goal

Improve one coherent form, wizard step, settings panel, filter form, checkout/signup form, or admin data-entry surface. The diff should reduce user error, clarify required action, preserve data safely, and align client UI with server contracts.

## Scope selection

- If the user named a form, field, validation issue, wizard, settings page, or submission failure, polish that surface and directly affected states.
- If the request is broad, inspect high-impact forms and choose the highest-confidence fix with completion, safety, or support impact.
- Include related copy, validation, accessibility, loading/error/success states, tests, i18n, and analytics hooks when they belong to the same form problem.
- Avoid backend contract changes, new form libraries, full redesigns, and unrelated field/schema changes unless required by the selected issue.

## Polish targets

- Labels, helper text, placeholders, required/optional clarity, units, formats, examples, masks, defaults, autofill, and persistence of unsaved input.
- Validation timing, inline errors, field-level vs form-level errors, server error mapping, disabled/submit/pending states, duplicate submission prevention, and retry/recovery.
- Multi-step flows: step order, progress, back/continue behavior, draft state, confirmation, and completion/next-step messages.
- Dangerous changes: confirmations, previews, irreversible action copy, permission/plan gates, and audit-friendly diagnostics.
- Accessibility: field associations, error announcements, focus movement after submit/error, keyboard operation, and semantic grouping.
- Directly affected tests, snapshots, localization catalogs, and docs when the repo uses them.

## Implementation principles

- Reuse existing validation schemas, form components, route actions, API error contracts, i18n, and state-management patterns.
- Keep client validation consistent with server validation; do not invent allowed values or business rules.
- Preserve user-entered data on recoverable errors whenever the repo architecture supports it.
- Fix the owner schema/component where repeated form issues share a source of truth.

## Validation

Run relevant repository-native checks. When possible, manually trace success, validation failure, server failure, pending, and retry states. Use preview/screenshot tooling when available.

## Final response

Respond in Russian with compact emoji sections: ♻️ changed form surface, 📁 key files, 🔎 evidence anchors, 🧪 checks, 👀 manual form trace, ⚠️ assumptions/risks, ⛔ not run/not included.
