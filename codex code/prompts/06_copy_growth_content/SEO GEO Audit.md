# SEO GEO Audit

## Mode

- Use the active `AGENTS.md` chain.
- Plan mode only: inspect the repository, do not edit product code.

## Goal

Audit public discoverability for search engines and generative-answer surfaces: crawlability, metadata, canonical URLs, structured data, content hierarchy, internal links, public trust evidence, performance-sensitive rendering, and regression coverage. Keep only issues with current repo evidence and public-surface impact.

## Inspect

Public routes/pages, route metadata, SSR/SSG/static generation, robots rules, sitemap generation, canonical/hreflang links, redirects, Open Graph/Twitter metadata, schema.org/JSON-LD, headings/content hierarchy, public docs/blog/FAQ/help content, landing copy, pricing/trust/legal pages, image alt text, internal links, analytics/search console hooks when repo-visible, tests/snapshots, and deployment/runtime config that affects public rendering.

## Issue classes

Look for concrete, reachable issues in:

- Crawlability and indexing: important public route blocked by robots/noindex/auth/client-only rendering, sitemap missing/stale, broken canonical, redirect loops, duplicate public URLs, and environment-specific metadata leakage.
- Metadata and snippets: missing/wrong title/description, OG/Twitter drift, weak or false public summaries, missing alt text for meaningful public images, and locale/hreflang inconsistencies.
- Structured data: missing, invalid, duplicated, or misleading JSON-LD/schema where the repo already has suitable public entities such as organization, product, article, FAQ, breadcrumb, software app, or local business.
- Content hierarchy and GEO: public pages lack clear answerable structure, entity definitions, FAQs, source/evidence sections, product capability boundaries, or trust signals needed for extraction by search and answer engines.
- Performance and rendering: public content or metadata depends on slow/failed client fetches, heavy media, or hydration-only rendering when the framework supports safer server/static output.
- Regression resistance: no tests/snapshots for critical metadata, sitemap, canonical, structured data, or public route rendering where repo patterns support them.

## Priority model

### P0

Primary public route cannot be indexed or renders materially wrong metadata/content, canonical/noindex blocks acquisition, legal/pricing/trust claim is false, or public content leaks private/internal data.

### P1

Important discoverability issue: stale sitemap/canonical/hreflang, missing metadata/structured data on high-value pages, weak answer-extraction structure on core public content, or missing regression coverage for critical metadata.

### P2

Lower-risk but concrete public-surface improvement: minor snippet drift, alt/internal-link gap, FAQ/schema opportunity backed by existing content, stale docs, or localized SEO inconsistency.

## Task-sub quality

- Use native Codex Cloud task-sub creation when available; do not force a handmade markdown task-sub body.
- Every task-sub must cite `path:line[-line]` evidence for the public route/content/metadata owner and affected surface, plus symbol when possible.
- Include expected rendered output, public user/search/answer impact, acceptance criteria, and validation direction.
- Use one unambiguous fix direction per task-sub; no alternatives.
- Merge symptoms under the same public route or metadata owner unless fixes, rollout units, locales, or validation differ.
- Do not recommend keyword stuffing, fake claims, hidden text, doorway pages, or generic content rewrites without repo-backed product truth.

## Output contract

Produce only native Codex Cloud task-subs grouped by P0/P1/P2. If none qualify, output each priority with `None`. Do not print a custom task-sub schema.
