# DESIGN.md Generation

## Mode

- Use the active `CLAUDE.md` context if present, then repository evidence.
- Work in the current Claude Code Cloud session. Do not assume hidden background runs or extra delegation mechanisms unless the user explicitly provides them.
- Implementation/documentation mode: generate or update `DESIGN.md` from actual UI/design evidence only.

## Goal

Create a practical design-system and UX reference for the current repository: tokens, components, layouts, interaction states, accessibility, content style, and implementation map.

## Inspect

UI source, components, style/theme files, tokens, CSS/Tailwind/config, Storybook/docs if present, design assets, screenshots/public assets, route/page structure, forms/tables/modals, i18n/copy, tests, generated artifacts, and existing docs.

## Content rules

- Prefer current source over stale docs.
- Do not invent colors, components, layouts, breakpoints, or design principles not evidenced in the repo.
- Separate direct evidence from inferred conventions; cite important source facts with `path:line[-line]` plus symbol when possible.
- Keep guidance actionable for future implementation, not a marketing description.
- Write in the repository’s dominant documentation language unless the user requests another language.

## Markdown structure

Use sections that fit the repo and omit irrelevant ones: overview, design sources inspected, tokens, layout/responsiveness, components and variants, navigation/information architecture, forms and validation UI, tables/lists/data visualization, icons/assets/media, interaction states, accessibility, content style, implementation map, QA checklist, and open questions.

Keep the artifact scannable: one H1, H2/H3 hierarchy, compact lists, small tables for token/component matrices, and no placeholder sections.

## Validation

After writing, verify references to files, classes, tokens, and components.

## Final response

Respond in Russian with compact emoji sections: ✅ DESIGN changed, 📁 key files, 🔎 key evidence anchors/assumptions, 🧪 checks, ⚠️ unknowns/risks.
