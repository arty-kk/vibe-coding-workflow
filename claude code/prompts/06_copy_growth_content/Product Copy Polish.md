# Product Copy Polish — In-App Clarity, Microcopy, and Trust

## Mode

- Use the active `CLAUDE.md` context if present, then repository evidence.
- Work in the current Claude Code Cloud session. Do not assume hidden background runs or extra delegation mechanisms unless the user explicitly provides them.
- Implementation mode: change the repository when a focused in-product copy improvement is justified by current evidence.

## Goal

Improve a coherent in-app copy surface so users understand what is happening, what they can do, what changed, and how to recover. This is for product microcopy; use `Landing Copy Polish.md` for public marketing pages and `SEO GEO Polish.md` for public search/answer surfaces.

## Scope selection

- If the user named a page, component, flow, role, plan state, error class, or terminology issue, polish that copy surface and directly affected states.
- If the request is broad, inspect user-facing surfaces and apply the highest-confidence copy improvements with task-completion, safety, trust, or support impact.
- Include related labels, helper text, state copy, validation messages, notifications, headings, and i18n keys when they belong to the same surface.
- Avoid visual redesigns, feature changes, and marketing claims unless required by the selected copy problem.

## Copy targets

- Navigation labels, headings, CTAs, button text, form labels, helper text, validation messages, empty/loading/error/disabled/no-access/no-plan/over-quota/destructive states.
- Toasts, banners, dialogs, confirmations, emails/notifications when repo-managed and directly tied to the same flow.
- Terminology consistency across roles, plans, tenants/workspaces/projects, entities, billing, AI-generated content, privacy/security boundaries, and support diagnostics.
- Truthfulness: copy must match implemented behavior, limits, pricing/plan state, permissions, data retention, and backend contracts.
- Localization: source strings, keys, interpolation, pluralization, and translated state coverage when the repo uses catalogs.

## Implementation principles

- Prefer source-of-truth copy, constants, i18n catalogs, and shared components over scattered literals.
- Make copy concrete, short, action-oriented, and user-safe; avoid hype, vague promises, internal jargon, and raw technical diagnostics.
- Preserve product terminology unless repo evidence shows current terminology is inconsistent or misleading.
- Update directly affected tests, snapshots, docs, and localization catalogs when the repo uses them.

## Validation

Run relevant repository-native checks. For UI copy changes, use preview/screenshot tooling when available; otherwise state the limitation. Verify no translated/interpolated string is broken when catalogs exist.

## Final response

Respond in Russian with compact emoji sections: ♻️ changed copy surface, 📁 key files, 🔎 evidence anchors, 🧪 checks, 👀 manual review/trace, ⚠️ assumptions/risks, ⛔ not run/not included.
