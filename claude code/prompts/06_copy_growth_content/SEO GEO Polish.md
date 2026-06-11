# SEO GEO Polish — Public Metadata, Content Structure, and Answerability

## Mode

- Use the active `CLAUDE.md` context if present, then repository evidence.
- Work in the current Claude Code Cloud session. Do not assume hidden background runs or extra delegation mechanisms unless the user explicitly provides them.
- Implementation mode: change the repository when a focused public discoverability improvement is justified by current evidence.

## Goal

Improve one coherent public route or content cluster for search and generative-answer discovery without inventing claims. The diff should align rendered content, metadata, structured data, canonical/sitemap behavior, and trust evidence for the selected surface.

## Scope selection

- If the user named a route, landing page, article, docs page, pricing/trust page, locale, metadata issue, or SEO/GEO goal, polish that surface and directly affected public artifacts.
- If the request is broad, inspect public routes and apply the highest-confidence improvement with discoverability, snippet, trust, or conversion impact.
- Include related copy hierarchy, metadata, schema, canonical/hreflang, sitemap, OG/Twitter, alt text, internal links, and tests when they belong to the same public surface.
- Avoid broad content strategy, fake claims, keyword stuffing, hidden text, backlink work, analytics-platform setup, and visual redesigns unless the task requires them.

## Polish targets

- Titles, descriptions, headings, summaries, FAQs, entity definitions, comparison/feature sections, pricing/trust/legal copy, and evidence-backed claims.
- Metadata and generated artifacts: canonical, hreflang, robots/noindex, sitemap entries, OG/Twitter cards, JSON-LD/schema, breadcrumbs, image alt text.
- Rendering: server/static availability of public content and metadata where the framework/repo pattern supports it.
- Localization: locale-specific metadata, translated public copy, hreflang consistency, and region-specific claims only when repo evidence supports them.
- Regression coverage: metadata/schema snapshots or route-render tests where the repo has a pattern.

## Implementation principles

- Keep all public claims truthful and backed by implemented product behavior, existing docs, pricing/config, or explicit repo content.
- Reuse existing metadata helpers, route conventions, content sources, design components, and i18n architecture.
- Prefer structured, answerable content over stuffing repeated keywords.
- Do not expose private routes, internal IDs, stack traces, draft content, or environment-specific URLs.
- Update directly affected tests, docs, generated artifacts, and localization catalogs when the repo uses them.

## Validation

Run relevant repository-native checks. When possible, render or inspect the affected public route/artifact to verify metadata, canonical, schema, sitemap, and visible content. State any limitation such as missing build, deploy URL, or crawler tooling.

## Final response

Respond in Russian with compact emoji sections: ♻️ changed public surface, 📁 key files, 🔎 evidence anchors, 🧪 checks/artifact validation, 👀 rendered/manual review, ⚠️ assumptions/risks, ⛔ not run/not included.
