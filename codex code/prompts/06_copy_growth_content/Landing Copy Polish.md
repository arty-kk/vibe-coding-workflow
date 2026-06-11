# Landing Copy Polish — Conversion, Clarity, and Trust

## Mode

- Use the active `AGENTS.md` chain.
- Execute mode: change the repository when changes are justified by current evidence.

## Goal

Improve a coherent landing/public marketing surface so the page communicates the product, audience, value, CTA, trust, and next step clearly without inventing unsupported claims.

## Scope selection

- If the user named a page/section, polish that surface and directly affected states.
- If the request is broad, inspect public landing/auth/onboarding entry surfaces and apply the highest-confidence improvements.
- Include related UX hierarchy, CTA, pricing/trust/FAQ, empty/error/public forms, and i18n fixes when they belong to the same public journey.
- Avoid new marketing claims, pricing changes, analytics vendors, visual redesigns, or backend work unless required by the requested surface.

## Copy targets

- Hero message, audience, problem, value proposition, CTA hierarchy, social proof/trust, feature framing, objections, FAQ, pricing teasers, onboarding handoff.
- Section order, headings, subheads, button labels, form labels, helper text, validation/error copy, legal/privacy-sensitive text, and microcopy.
- Consistency between public claims and actual product behavior, plans, integrations, screenshots, docs, or code.
- Accessibility and scanability: semantic headings, link purpose, alt text, readable lengths, and localized content where the repo supports it.

## Implementation principles

- Reuse existing content style, components, route conventions, i18n architecture, assets, and design tokens.
- Prefer specific truthful copy over generic hype.
- Keep product claims backed by repo evidence or existing docs/assets.
- Update directly affected tests, snapshots, localization catalogs, and docs when the repo uses them.

## Validation

Run relevant repository-native checks. When explaining non-obvious repo facts, skipped adjacent work, or detected behavior, cite `path:line[-line]` where useful.

Use preview/screenshot tooling when available; otherwise state the limitation.

## Final response

Respond in Russian with compact emoji sections: ♻️ changed surfaces, 📁 key files, 🧪 checks, 👀 manual review/trace, ⚠️ assumptions/risks, ⛔ not run/not included.
