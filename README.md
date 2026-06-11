# Vibe-coding Workflow — финальный набор ручных промпт-скилов

Этот архив — финальная версия внешнего набора ручных промптов для работы с coding agents. Он предназначен не для копирования целиком в репозиторий, а для ручной вставки отдельных промптов в чат с агентом.

В репозитории должен лежать только один durable-файл под конкретный агент:

```text
codex code/AGENTS.md                  → положить в root репозитория как AGENTS.md
claude code/CLAUDE.md      → положить в root репозитория как CLAUDE.md
```

Правило изоляции: для одной рабочей сессии и одного репозитория активен только один durable-файл. Если работа идёт в Codex, используется только `AGENTS.md`. Если работа идёт в Claude Code Cloud, используется только `CLAUDE.md`. Эти файлы не должны импортировать друг друга, ссылаться друг на друга, быть symlink-ами друг на друга или использоваться как fallback друг для друга.

Все остальные файлы из `prompts/` используются вручную: открыть нужный `.md`, вставить его в чат с агентом и добавить текущий контекст задачи, ссылку на diff, вывод предыдущего аудита или короткое описание scope.

## Что считать финальной версией

Финальная версия — этот архив с root-level `README.md` и двумя ветками:

```text
codex code/
claude code/
```

## Структура архива

```text
vibe_coding_workflow/
  README.md

  codex code/
    
      AGENTS.md
    prompts/
      00_core_intake_synthesis/
      01_review_quality_gates/
      02_repository_maps/
      03_backend_api_bot/
      04_product_ui_ux/
      05_design_a11y_visual/
      06_copy_growth_content/
      07_ai_ml_rag_ocr/
      08_infra_ops_jobs/
      09_business_rules_data_analytics/
      10_docs_refactor_generation/
      11_reliability_consistency_perf/

  claude code/
    
      CLAUDE.md
    prompts/
      00_core_intake_synthesis/
      01_review_quality_gates/
      02_repository_maps/
      03_backend_api_bot/
      04_product_ui_ux/
      05_design_a11y_visual/
      06_copy_growth_content/
      07_ai_ml_rag_ocr/
      08_infra_ops_jobs/
      09_business_rules_data_analytics/
      10_docs_refactor_generation/
      11_reliability_consistency_perf/
```

Ветки `codex` и `claude` содержат одинаковые по назначению ручные промпты. Отличается только платформа: Codex-версия ориентирована на Codex, Claude-версия адаптирована под Claude Code Cloud и не предполагает нативных `task-sub`-возможностей.

## Как использовать Codex-ветку

1. Положить `codex code/AGENTS.md` в root проекта как `AGENTS.md`. Не добавлять и не импортировать второй durable-файл для другого агента.
2. Для конкретной задачи брать один файл из `codex code/prompts/`.
3. Вставлять этот файл в чат с Codex вместе с конкретным контекстом: задача, diff, ошибки, audit output, scope или ссылки на файлы.
4. Не вставлять весь архив целиком.
5. После значимого изменения запускать `01_review_quality_gates/Patch Checking.md`.

## Как использовать Claude Code Cloud-ветку

1. Положить `claude code/CLAUDE.md` в root проекта как `CLAUDE.md`. Не добавлять и не импортировать второй durable-файл для другого агента.
2. Для конкретной задачи брать один файл из `claude code/prompts/`.
3. Вставлять этот файл в чат с Claude Code Cloud вместе с контекстом задачи.
4. Не ожидать нативных task-sub. Audit-промпты в Claude-ветке должны выдавать обычные chat work items, которые можно вручную использовать в следующем сообщении.
5. После значимого изменения запускать `01_review_quality_gates/Patch Checking.md`.

## Главная модель работы

Набор построен вокруг четырёх типов промптов:

```text
Audit      → найти проблемы, риски, дефекты, gaps; код по умолчанию не менять.
Polish     → исправить один выбранный owner-layer slice с проверкой результата.
Synthesis  → объединить несколько audit outputs и выбрать приоритетный scope.
Checking   → проверить уже сделанный patch на регрессии, contracts и missed validation.
```

Практическое правило:

```text
непонятно, где проблема       → Audit
понятно, что надо чинить      → Polish
много найденных проблем       → Synthesis.md
что-то уже изменено           → Patch Checking.md
надо превратить запрос в ТЗ   → Task Shaping.md
есть неоднозначность          → Validation & Clarification.md
```

## Форматы связок

### Формат `1 → done`

Использовать, когда задача маленькая, поверхность понятна, риск низкий, а expected output очевиден.

Примеры:

```text
UI Polish.md
```

```text
Product Copy Polish.md
```

```text
Patch Checking.md
```

Важно: `Patch Checking.md` должен брать весь patch range (`merge-base(base, HEAD)..HEAD` + working tree overlay), а не только последний commit.

Подходит для точечных правок. Не подходит, если затронуты права, данные, транзакции, очередь, кэш, платежи, RAG/OCR pipeline или несколько owner layers.

### Формат `1 → 2`

Использовать, когда сначала нужно найти точную проблему, а потом чинить.

```text
Audit
→ Polish
```

Примеры:

```text
Queue Workflow Audit.md
→ Queue Workflow Polish.md
```

```text
UX Flow Audit.md
→ UX Flow Polish.md
```

```text
SEO GEO Audit.md
→ SEO GEO Polish.md
```

### Формат `1 → 2 → 3`

Использовать, когда после реализации нужна обязательная проверка patch-level contracts.

```text
Audit
→ Polish
→ Patch Checking
```

Примеры:

```text
Transaction Boundary Audit.md
→ Transaction Boundary Polish.md
→ Patch Checking.md
```

```text
Data Isolation Audit.md
→ Data Isolation Polish.md
→ Patch Checking.md
```

```text
RAG Audit.md
→ RAG Polish.md
→ Patch Checking.md
```

### Формат `1 → ... → n`

Использовать для комплексных задач, где одна проблема может проходить через несколько систем: API, DB, queue, cache, UI, analytics, external provider, RAG index, storage или permissions.

Общий шаблон:

```text
Navigation / Audit
→ domain Audit
→ соседний domain Audit, если риск пересекается
→ Synthesis
→ один выбранный Polish
→ Patch Checking
→ Release Readiness Audit, если это pre-ship
```

Важно: при нескольких audit outputs не запускай несколько polish-промптов подряд без `Synthesis.md`. Сначала нужно выбрать один coherent scope.

## Повторный запуск polish-промптов

Все `*Polish.md` должны работать с внутренним этапом выбора цели.

Правило repeat-run priority:

```text
1. Собрать candidates из запроса, prior scope, audit output, текущего diff и repo evidence.
2. Разложить candidates по P0/P1/P2.
3. Если пользователь явно назвал цель — чинить её, если она валидна и не противоречит scope.
4. Если цель не названа — выбрать unresolved P0.
5. Если P0 нет — выбрать unresolved P1.
6. Если P1 нет — выбрать unresolved P2.
7. Не полировать P2, пока в prior scope остался P0 или P1.
8. Не чинить уже resolved item повторно ради косметики.
9. По умолчанию править один coherent owner-layer slice.
```

Это защищает от частого агентного регресса: повторный запуск polish-промпта начинает улучшать соседние мелочи, пока исходная P0/P1-проблема ещё не закрыта.

## Уровни приоритета

```text
P0 — correctness/security/data-loss/tenant-leak/prod-blocker/irreversible side-effect.
P1 — broken main flow, serious reliability issue, high user impact, bad observability around critical path.
P2 — polish, maintainability, UX clarity, performance improvement without proven urgent impact.
```

Если агент не может доказать приоритет через repo evidence, он должен честно пометить неопределённость, а не завышать severity.

## Лучшие связки по задачам

### Быстро понять незнакомый репозиторий

Когда применять: новый проект, большой legacy repo, нужно быстро понять основные owner layers и entrypoints.

```text
SaaS Navigation Map.md / API Navigation Map.md / AI Navigation Map.md / Bot Navigation Map.md
→ Task Shaping.md
```

Что даёт: карту surface, entrypoints, flows, contracts, тестов и рисков без немедленных правок.

### Сформировать качественную задачу из сырого запроса

Когда применять: запрос расплывчатый, есть много вариантов реализации, нужно подготовить один хороший implementation prompt.

```text
Validation & Clarification.md
→ Task Shaping.md
```

Если вопросов слишком много, сначала использовать `Validation & Clarification.md`, затем собрать один плотный task brief через `Task Shaping.md`.

### Объединить несколько аудитов

Когда применять: есть несколько audit outputs, они пересекаются или конфликтуют.

```text
Synthesis.md
→ выбранный Polish.md
→ Patch Checking.md
```

Что даёт: дедупликацию, приоритизацию и выбор одного coherent slice для реализации.

### Проверить сделанный patch

Когда применять: после любого meaningful code change.

```text
Patch Checking.md
```

Что проверяет: producer/consumer contracts, реальные call paths, validation, tests, migration impact, regressions, scope creep и fake validation.

### Pre-ship проверка

Когда применять: перед merge/release/deploy, особенно после изменений в auth, billing, jobs, DB, AI pipeline или public UI.

```text
Patch Checking.md
→ Release Readiness Audit.md
```

Если `Release Readiness Audit.md` находит P0/P1, сначала чинить их через соответствующий domain Polish, затем снова запускать `Patch Checking.md`.

## Надёжность, очереди, транзакции, кэш, консистентность

### Очереди, workers, cron, redelivery

Когда применять: есть queue/job/worker/cron/webhook consumer, повторные доставки, retries, DLQ, async status или long-running processing.

```text
Queue Workflow Audit.md
→ Idempotency Audit.md
→ Transaction Boundary Audit.md
→ Cross-System Consistency Audit.md
→ Synthesis.md
→ Queue Workflow Polish.md / Idempotency Polish.md
→ Patch Checking.md
```

Короткая аннотация:

```text
Queue Workflow Audit      — ищет проблемы producer/consumer contract, retries, ack/commit, DLQ, leases, payload scope.
Queue Workflow Polish     — чинит один queue/workflow slice без мифа exactly-once.
Idempotency Audit         — проверяет duplicate requests, redelivery, webhooks, replay response, dedupe scope.
Transaction Boundary Audit— проверяет atomicity и commit/side-effect ordering.
Cross-System Consistency  — проверяет drift между DB, queue, cache, search, webhook, email, payment.
```

### Транзакции базы и инварианты

Когда применять: деньги, квоты, ownership, status transitions, counters, inventory, subscriptions, imports, state machines.

```text
Transaction Boundary Audit.md
→ Concurrency Race Audit.md
→ Data Model Audit.md
→ Synthesis.md
→ Transaction Boundary Polish.md / Concurrency Race Polish.md
→ Patch Checking.md
```

Короткая аннотация:

```text
Transaction Boundary Audit  — ищет check-then-write races, wrong isolation, missing constraints/locks, side effects inside transaction.
Concurrency Race Audit      — ищет lost update, double processing, overlapping workers, stale overwrite, process-local lock bugs.
Data Model Audit            — проверяет schema, indexes, migrations, invariants, ORM drift.
Transaction Boundary Polish — чинит один атомарный boundary с tests/fixtures.
```

Важно: не использовать `Serializable everywhere` как замену пониманию инварианта. Сначала определить invariant и реальный механизм защиты: constraint, atomic update, row/advisory lock, optimistic versioning, lease или retry loop.

### Идемпотентность

Когда применять: payment/webhook/import/export/upload/AI ingestion/queue redelivery/API mutation/double-submit.

```text
Idempotency Audit.md
→ Transaction Boundary Audit.md
→ Queue Workflow Audit.md, если есть async consumer
→ Idempotency Polish.md
→ Patch Checking.md
```

Короткая аннотация:

```text
Idempotency Audit   — проверяет dedupe scope, replay response, concurrent duplicates, irreversible side effects.
Idempotency Polish  — добавляет корректный idempotency boundary без UI-only debounce и in-memory flags.
```

Главное правило: idempotency key должен иметь правильный scope: tenant/user/resource/operation/provider. Дедупликация после irreversible side effect — не идемпотентность.

### Кэш

Когда применять: Redis/app cache/CDN/browser cache/RAG cache/search cache/vector cache, performance optimization через cache, stale data, private data leakage.

```text
Cache Strategy Audit.md
→ Data Isolation Audit.md, если есть private/tenant/role/plan data
→ Performance Audit.md, если цель скорость
→ Cache Strategy Polish.md
→ Patch Checking.md
```

Короткая аннотация:

```text
Cache Strategy Audit   — проверяет key scope, invalidation, TTL/stale/error policy, stampede, private/public boundary.
Cache Strategy Polish  — чинит один cache boundary с correctness-first подходом.
Data Isolation Audit   — проверяет tenant/user/role scope в cache/search/storage/export.
Performance Audit      — подтверждает, что cache действительно нужен для hot path.
```

Главное правило: не добавлять кэш до определения owner, key scope, invalidation, stale behavior и observability.

### Изоляция данных и multi-tenant boundaries

Когда применять: tenant/workspace/project/user/role/plan data, signed URLs, exports, search/vector indexes, storage paths, admin/support paths.

```text
Data Isolation Audit.md
→ Auth Permissions Audit.md
→ Cache Strategy Audit.md, если есть derived/private cache/index/search
→ Data Isolation Polish.md / Auth Permissions Polish.md
→ Patch Checking.md
```

Короткая аннотация:

```text
Data Isolation Audit       — ищет leaks в API, DB queries, cache keys, storage, search, exports, jobs, analytics.
Auth Permissions Audit     — проверяет permission model, role/plan gates, no-access semantics, API/UI mismatch.
Data Isolation Polish      — чинит один data boundary end-to-end.
Auth Permissions Polish    — чинит owner checks, role checks, forbidden/not-found semantics и UI states.
```

Главное правило: UI hiding и route guards не являются authorization. Проверка должна быть server-side и распространяться на derived surfaces.

### Performance hot path

Когда применять: есть измеримый bottleneck или явный hot path: медленный endpoint, N+1, waterfall, blocking work, huge payload, slow hydration, queue amplification.

```text
Performance Audit.md
→ Cache Strategy Audit.md / Transaction Boundary Audit.md / External Dependency Reliability Audit.md, если bottleneck туда указывает
→ Performance Hot Path Polish.md
→ Patch Checking.md
```

Короткая аннотация:

```text
Performance Audit          — ищет реальные bottlenecks, а не generic advice.
Performance Hot Path Polish— чинит один доказанный hot path: query, index, pagination, waterfall, blocking call, bundle, cache boundary.
```

Главное правило: не оптимизировать наугад. Сначала найти repo evidence, measurement, trace, query plan, bundle diff, log или воспроизводимый path.

### Внешние зависимости и провайдеры

Когда применять: payments, email, storage, AI/OCR/RAG provider, rate limits, timeout ambiguity, SDK wrappers, transient failures.

```text
External Dependency Reliability Audit.md
→ Idempotency Audit.md, если есть mutation/webhook
→ Cross-System Consistency Audit.md, если есть side effects
→ External Dependency Reliability Polish.md
→ Patch Checking.md
```

Короткая аннотация:

```text
External Dependency Reliability Audit  — проверяет timeouts, deadlines, retry budget, backoff/jitter, ambiguous success, rate limits.
External Dependency Reliability Polish — чинит один provider boundary с правильной обработкой retry/fallback/observability.
```

Главное правило: retries без idempotency и bounded retry budget могут усилить инцидент.

### Cross-system consistency

Когда применять: DB + queue, DB + cache, DB + search, DB + vector index, DB + email, DB + payment, DB + webhook.

```text
Cross-System Consistency Audit.md
→ Queue Workflow Audit.md
→ Idempotency Audit.md
→ Cross-System Consistency Polish.md
→ Patch Checking.md
```

Короткая аннотация:

```text
Cross-System Consistency Audit  — ищет drift между source of truth и derived/side-effect systems.
Cross-System Consistency Polish — чинит ordering, outbox/reconciliation/backfill/invalidation/status visibility для одного flow.
```

Главное правило: не создавать два источника истины. Consumer не должен заново принимать domain decisions, если они уже принадлежат source of truth.

## Backend, API, bot

### API contract

Когда применять: endpoint schema, validation, error model, pagination, idempotency, client compatibility.

```text
API Audit.md
→ API Polish.md
→ Patch Checking.md
```

Если API mutation связана с деньгами, квотами, jobs или external provider:

```text
API Audit.md
→ Idempotency Audit.md
→ Transaction Boundary Audit.md
→ API Polish.md / Idempotency Polish.md
→ Patch Checking.md
```

### Bot / chat integration

Когда применять: Telegram/Discord/Slack/WhatsApp бот, command routing, webhook delivery, retries, user state.

```text
Bot Audit.md
→ Queue Workflow Audit.md, если есть async processing
→ Bot Polish.md
→ Patch Checking.md
```

## UI, UX, design, copy

### UI polish

Когда применять: визуальная поверхность выглядит сырой, inconsistent, broken on mobile, spacing/hierarchy/states плохие.

```text
UI Surface Audit.md
→ UI Polish.md
→ Patch Checking.md
```

Короткая аннотация:

```text
UI Surface Audit — ищет UI defects без правок.
UI Polish        — чинит hierarchy, spacing, responsive, states, component consistency, token fit.
```

Не использовать `UI Polish.md` для перепроектирования user journey. Для этого есть `UX Flow Audit.md` и `UX Flow Polish.md`.

### UX flow

Когда применять: пользователь не понимает next step, застревает, не видит feedback, recovery, completion или state transition.

```text
UX Flow Audit.md
→ Product Copy Polish.md / Form UX Polish.md / Data UI Polish.md, если проблема локальная
→ UX Flow Polish.md
→ Patch Checking.md
```

Короткая аннотация:

```text
UX Flow Audit  — проверяет entry → action → validation → feedback → recovery → completion.
UX Flow Polish — чинит один сценарий прохождения, не превращая задачу в redesign.
```

### Формы

Когда применять: формы, настройки, wizard, validation, autosave, errors, disabled states.

```text
Form UX Polish.md
→ Patch Checking.md
```

Если форма связана с billing/auth/data mutation:

```text
Form UX Polish.md
→ Auth Permissions Audit.md / Idempotency Audit.md
→ Patch Checking.md
```

### Data UI

Когда применять: таблицы, списки, фильтры, сортировка, bulk actions, empty/error/loading states, export.

```text
Data UI Polish.md
→ Data Isolation Audit.md, если есть private/tenant data
→ Patch Checking.md
```

### Design system

Когда применять: tokens, components, variants, Tailwind/theme drift, duplicate ad-hoc styles.

```text
Design System Audit.md
→ Design System Polish.md
→ Visual Regression Harness.md, если есть screenshot tooling
→ Patch Checking.md
```

Короткая аннотация:

```text
Design System Audit  — ищет drift между компонентами, токенами, variants и реальным UI.
Design System Polish — чинит component/token boundary без ad-hoc style sprawl.
```

### Accessibility

Когда применять: keyboard navigation, focus, semantic HTML, labels, screen reader states, color contrast, error announcement.

```text
Accessibility Audit.md
→ Accessibility Polish.md
→ Patch Checking.md
```

### Copy, landing, SEO/GEO

Когда применять: текст интерфейса, лендинг, metadata, публичные страницы, answerability для search/LLM surfaces.

```text
Product Copy Polish.md
→ Patch Checking.md
```

```text
Landing Copy Polish.md
→ SEO GEO Audit.md
→ SEO GEO Polish.md
→ Patch Checking.md
```

Короткая аннотация:

```text
Product Copy Polish — чинит microcopy, labels, errors, empty states, CTAs.
Landing Copy Polish — чинит структуру и убедительность публичной страницы.
SEO GEO Audit       — проверяет crawlability, metadata, canonical, schema, sitemap, public answerability.
SEO GEO Polish      — чинит один public growth surface без keyword stuffing.
```

## AI, ML, OCR, RAG

### AI feature

Когда применять: model calls, prompts, structured outputs, tool usage, streaming, retries, cost/rate limits, safety/privacy.

```text
AI Navigation Map.md
→ AI Feature Audit.md
→ AI Eval Harness.md
→ выбранный Polish.md
→ Patch Checking.md
```

Короткая аннотация:

```text
AI Navigation Map — показывает AI entrypoints, model boundaries, data flow и eval points.
AI Feature Audit  — ищет defects в model calls, schemas, prompt/tool contracts, safety, cost, retries.
AI Eval Harness   — добавляет deterministic fixtures/evals там, где это возможно.
```

### RAG

Когда применять: ingestion, chunking, embeddings, retrieval, rerank, citations, freshness, ACL, vector index.

```text
AI Navigation Map.md
→ RAG Audit.md
→ Data Isolation Audit.md, если есть private corpus
→ RAG Polish.md
→ AI Eval Harness.md
→ Patch Checking.md
```

Короткая аннотация:

```text
RAG Audit  — ищет проблемы ingestion/retrieval/citations/freshness/ACL.
RAG Polish — чинит один RAG slice: indexing, retrieval, prompt grounding, citations или eval fixture.
```

### LLM agents and tools

Когда применять: tool/function schemas, agent loops, approvals, mutation tools, tool permissions, prompt-injection-to-tool risks.

```text
LLM Agent Tools Audit.md
→ Data Isolation Audit.md
→ Idempotency Audit.md, если tools мутируют состояние
→ AI Eval Harness.md
→ выбранный Polish.md
→ Patch Checking.md
```

Короткая аннотация:

```text
LLM Agent Tools Audit — проверяет tool schemas, approvals, permissions, loops, retries, traceability и tool-choice evals.
```

### OCR / Document AI

Когда применять: file intake, OCR extraction, confidence, layout, human correction, export, PII, retries.

```text
OCR Document AI Audit.md
→ Data Isolation Audit.md, если документы private/tenant-scoped
→ OCR Document AI Polish.md
→ AI Eval Harness.md
→ Patch Checking.md
```

### ML pipeline

Когда применять: train/eval/serve, dataset split, leakage, model registry, monitoring, data drift.

```text
ML Pipeline Audit.md
→ AI Eval Harness.md
→ Performance Audit.md, если serving latency важна
→ выбранный Polish.md
→ Patch Checking.md
```

## Infra, observability, jobs, deploy

### Infra ops

Когда применять: env/config, service topology, deploy assumptions, secrets, health checks, backups, migrations, rollbacks.

```text
Infra Ops Audit.md
→ Observability Polish.md / Deploy Bootstrap.md
→ Release Readiness Audit.md
```

Короткая аннотация:

```text
Infra Ops Audit      — ищет ops gaps без навязывания конкретной платформы.
Observability Polish — чинит logs/metrics/traces/health/runbook surface.
Deploy Bootstrap     — помогает подготовить deploy path, когда задача именно bootstrap deploy.
```

### Background jobs

Когда применять: async work, cron, workers, scheduled tasks, queue-like flows без глубокой queue-specific задачи.

```text
Background Jobs Audit.md
→ Queue Workflow Audit.md, если есть retries/redelivery/DLQ/leases
→ Background Jobs Polish.md / Queue Workflow Polish.md
→ Patch Checking.md
```

## Business rules, billing, permissions, analytics, data model

### Billing and entitlements

Когда применять: plans, subscriptions, limits, quota, payment provider, plan gates, trial states.

```text
Billing Entitlements Audit.md
→ Auth Permissions Audit.md
→ Idempotency Audit.md, если есть payment/provider webhook
→ Billing Entitlements Polish.md
→ Patch Checking.md
```

Короткая аннотация:

```text
Billing Entitlements Audit  — ищет plan/quota/subscription drift между backend, UI и provider.
Billing Entitlements Polish — чинит один entitlement boundary end-to-end.
```

### Permissions

Когда применять: RBAC, workspace/team/project ownership, no-access UI, forbidden/not-found semantics.

```text
Auth Permissions Audit.md
→ Data Isolation Audit.md
→ Auth Permissions Polish.md
→ Patch Checking.md
```

### Analytics and instrumentation

Когда применять: funnel visibility, event naming, missing events, duplicate events, privacy-sensitive analytics.

```text
Product Analytics Audit.md
→ Instrumentation Polish.md
→ Patch Checking.md
```

Короткая аннотация:

```text
Product Analytics Audit — проверяет event coverage, naming, funnel gaps, privacy and dedupe.
Instrumentation Polish  — добавляет/чинит один analytics boundary без спама событиями.
```

### Data model

Когда применять: schema, migrations, indexes, constraints, ORM mismatch, domain invariants.

```text
Data Model Audit.md
→ Transaction Boundary Audit.md, если есть atomicity/race risk
→ выбранный Polish.md
→ Patch Checking.md
```

## Документация и рефакторинг

### README / DESIGN generation

Когда применять: нужно создать или обновить документацию по фактическому repo evidence.

```text
README GEN.md
```

```text
DESIGN GEN.md
```

Правило: не писать aspirational docs. Документация должна отражать фактический код, команды, env, architecture и known gaps.

### Migration and refactor

Когда применять: перенос слоя, изменение архитектуры, удаление legacy paths, split/merge modules.

```text
Refactor Boundary Audit.md
→ domain Audit, если boundary связан с auth/data/jobs/AI/cache/API
→ Refactor Boundary Polish.md / Migration & Refactor.md
→ Patch Checking.md
```

Короткая аннотация:

```text
Refactor Boundary Audit  — ищет dangerous coupling, duplicated sources of truth, boundary drift.
Refactor Boundary Polish — чинит один refactor boundary без скрытого behavior change.
Migration & Refactor     — использовать для более явных migration/refactor задач.
```

Главное правило: refactor не должен скрывать изменение поведения. Если поведение меняется — это не чистый refactor, а migration или feature change.

## Как выбирать между похожими промптами

```text
Web Polish        — широкий web/product surface, когда проблема не узкая.
UI Polish         — визуальный слой: hierarchy, spacing, responsive, states, consistency.
UX Flow Polish    — сценарий пользователя: entry, action, feedback, recovery, completion.
Form UX Polish    — формы, wizard, validation, save/retry states.
Data UI Polish    — таблицы, lists, filters, bulk actions, exports.
Design System     — tokens/components/variants/theme drift.
Product Copy      — microcopy внутри продукта.
Landing Copy      — публичная страница и conversion narrative.
SEO GEO           — crawlability, metadata, schema, public answerability.
```

```text
Background Jobs   — общий async/job/cron слой.
Queue Workflow    — queue-specific reliability: redelivery, ack, retry, DLQ, leases.
Idempotency       — duplicate-safe mutation boundary.
Transaction       — DB atomicity/isolation/invariants.
Concurrency       — races across API/workers/webhooks/cache, не только DB.
Consistency       — drift между DB и derived/side-effect systems.
External Reliability — provider calls, timeouts, rate limits, ambiguous success.
```

```text
AI Feature        — общий AI surface.
RAG               — retrieval/indexing/citations/freshness/ACL.
OCR Document AI   — documents, layout, confidence, correction, export.
LLM Agent Tools   — tool schemas, approvals, mutation tools, tool security.
ML Pipeline       — train/eval/serve/data leakage/model monitoring.
```

## Как использовать индустриальные стандарты и best practices

Стандарты должны быть опорой, а не кашей правил. Промпт должен сначала определить домен и repo evidence, а уже потом применять подходящий стандарт.

Хорошие связки:

```text
HTTP semantics / idempotent methods        → API Audit, Idempotency Audit
HTTP caching / cache-control               → Cache Strategy Audit для browser/CDN/shared cache
DB isolation docs конкретной БД             → Transaction Boundary Audit
OWASP ASVS / Authorization guidance         → Security, Auth Permissions, Data Isolation
OpenTelemetry semantic conventions          → Observability, External Dependency Reliability, Queue Workflow
Core Web Vitals                             → Performance Audit для public/user-facing web
Cloud/provider retry guidance               → External Dependency Reliability, Queue Workflow, Idempotency
```

Плохие связки:

```text
HTTP cache rules как универсальное правило для Redis/app cache.
Serializable isolation как универсальный фикс всех race conditions.
DRY/SOLID как причина переписать рабочий бизнес-код без evidence.
Accessibility checklist как замена реальной keyboard/focus/error-state проверки.
SEO rules как keyword stuffing или генерация мусорных страниц.
Retry/backoff без idempotency и retry budget.
Cache как performance fix без invalidation и data isolation.
UI hiding как authorization.
```

Правило для агента: если стандарт применим только частично, он должен назвать границу применимости. Если стандарт конфликтует с фактической архитектурой проекта, сначала описать конфликт и выбрать минимальный безопасный шаг.

## Антипаттерны, которые встроены в durable files

В `AGENTS.md` и `CLAUDE.md` добавлен универсальный блок `Agent anti-patterns`. Его задача — не описывать домены, а предотвращать типичные регрессии агента:

```text
symptom-only patches
parallel source of truth
hidden fallback / broad catch / silent retry
scope creep
contract drift
UI-only enforcement
single-process / exactly-once assumptions
cache/retry/background work before correctness contract
standards cargo-cult
dead/stale paths
fake validation
buried uncertainty
```

Доменные anti-patterns живут внутри релевантных prompt-skills, а не в root repo files. Это сделано специально, чтобы `AGENTS.md` и `CLAUDE.md` оставались короткими durable contracts.

## Что не смешивать без Synthesis

Не запускать одновременно или подряд без `Synthesis.md`, если outputs пересекаются:

```text
UI Polish.md + UX Flow Polish.md + Product Copy Polish.md
```

```text
Cache Strategy Polish.md + Performance Hot Path Polish.md + Data Isolation Polish.md
```

```text
Queue Workflow Polish.md + Idempotency Polish.md + Cross-System Consistency Polish.md
```

```text
Auth Permissions Polish.md + Data Isolation Polish.md + Billing Entitlements Polish.md
```

```text
RAG Polish.md + Data Isolation Polish.md + AI Eval Harness.md
```

Сначала объединить findings через `Synthesis.md`, затем выбрать один owner-layer slice.

## Минимальный daily-набор

Для повседневной работы чаще всего достаточно:

```text
Task Shaping.md
Validation & Clarification.md
Synthesis.md
Patch Checking.md
Check & Fix Plan.md
Release Readiness Audit.md

UI Polish.md
UX Flow Polish.md
Design System Polish.md
Form UX Polish.md
Data UI Polish.md
Product Copy Polish.md

API Polish.md
Auth Permissions Audit.md
Data Model Audit.md

AI Feature Audit.md
LLM Agent Tools Audit.md
RAG Audit.md
RAG Polish.md
AI Eval Harness.md

Queue Workflow Audit.md
Transaction Boundary Audit.md
Idempotency Audit.md
Cache Strategy Audit.md
Data Isolation Audit.md
Performance Hot Path Polish.md
Cross-System Consistency Audit.md
External Dependency Reliability Audit.md
```

Остальные промпты доставать под конкретный домен.

## Каталог папок

```text
00_core_intake_synthesis
```

Формирование задачи, уточнение неоднозначности, синтез findings, улучшение существующего prompt/workflow.

```text
01_review_quality_gates
```

Проверки качества: patch review, security, performance, test coverage, release readiness, visual regression.

```text
02_repository_maps
```

Навигационные карты для SaaS/API/Bot/AI репозиториев. Использовать перед глубоким audit, если проект незнаком.

```text
03_backend_api_bot
```

API и bot surfaces: contracts, validation, error semantics, routing, webhook/command flows.

```text
04_product_ui_ux
```

UI, UX, forms, onboarding, data UI, SaaS/web polish.

```text
05_design_a11y_visual
```

Design system, accessibility, component/token consistency.

```text
06_copy_growth_content
```

Product copy, landing copy, localization, notification/email, SEO/GEO.

```text
07_ai_ml_rag_ocr
```

AI features, RAG, OCR/Document AI, LLM tools/agents, eval harness, ML pipeline.

```text
08_infra_ops_jobs
```

Infra, deploy bootstrap, observability, background jobs.

```text
09_business_rules_data_analytics
```

Auth, permissions, billing, entitlements, analytics, instrumentation, data model.

```text
10_docs_refactor_generation
```

Docs generation, migration/refactor, refactor boundary work.

```text
11_reliability_consistency_perf
```

Очереди, транзакции, кэш, идемпотентность, изоляция данных, concurrency, consistency, external dependency reliability, hot-path performance.

## Краткие аннотации ключевых файлов

```text
Task Shaping.md
```

Превращает сырой запрос в один плотный implementation prompt.

```text
Validation & Clarification.md
```

Находит ambiguity и missing constraints; помогает не начинать реализацию на неправильных предположениях.

```text
Synthesis.md
```

Объединяет несколько audit outputs, дедуплицирует findings и выбирает P0/P1/P2 scope.

```text
Patch Checking.md
```

Проверяет весь patch range, а не только последний commit: branch delta от merge-base к `HEAD` плюс staged/unstaged/untracked overlay. Ловит реальные contracts, missed validation, regressions и fake fixes.

```text
Check & Fix Plan.md
```

Строит практичный план исправления найденной проблемы без немедленного хаотичного кода.

```text
Release Readiness Audit.md
```

Pre-ship gate: проверяет, готово ли изменение к merge/release/deploy.

```text
Performance Audit.md
```

Ищет bottlenecks и performance risks по repo evidence.

```text
Performance Hot Path Polish.md
```

Чинит один доказанный hot path.

```text
Security Audit.md
```

Ищет security issues, но не должен заменять domain-specific Auth/Data Isolation prompts.

```text
Test Coverage Audit.md
```

Ищет gaps в unit/integration/e2e/regression coverage.

```text
Visual Regression Harness.md
```

Помогает добавить screenshot/visual checks там, где это поддержано проектом.

```text
API Audit.md / API Polish.md
```

Проверяют и улучшают API contracts, validation, error model, pagination, idempotency и client impact.

```text
Auth Permissions Audit.md / Auth Permissions Polish.md
```

Проверяют и чинят permission boundary, role/plan gates, tenant/workspace scoping.

```text
Data Isolation Audit.md / Data Isolation Polish.md
```

Проверяют и чинят private/multi-tenant data boundaries across API, DB, cache, storage, search, queue, export.

```text
Queue Workflow Audit.md / Queue Workflow Polish.md
```

Проверяют и чинят async queue/workflow reliability: retries, ack, DLQ, leases, poison messages, idempotent consumers.

```text
Transaction Boundary Audit.md / Transaction Boundary Polish.md
```

Проверяют и чинят DB atomicity/isolation/invariant boundaries.

```text
Idempotency Audit.md / Idempotency Polish.md
```

Проверяют и чинят duplicate-safe mutation boundaries.

```text
Cache Strategy Audit.md / Cache Strategy Polish.md
```

Проверяют и чинят cache ownership, key scope, invalidation, stale behavior и isolation.

```text
Cross-System Consistency Audit.md / Cross-System Consistency Polish.md
```

Проверяют и чинят consistency между source of truth и derived/side-effect systems.

```text
External Dependency Reliability Audit.md / External Dependency Reliability Polish.md
```

Проверяют и чинят provider boundary: timeouts, retries, rate limits, ambiguous success, fallback, observability.

```text
Refactor Boundary Audit.md / Refactor Boundary Polish.md
```

Отделяют полезный refactor от косметического churn и защищают от скрытого behavior change.

```text
AI Feature Audit.md
```

Проверяет model calls, prompts, schemas, tool contracts, retries, cost, safety и privacy.

```text
RAG Audit.md / RAG Polish.md
```

Проверяют и чинят RAG ingestion/retrieval/citations/freshness/ACL/eval.

```text
LLM Agent Tools Audit.md
```

Проверяет tool schemas, approval boundaries, mutation tools, prompt-injection-to-tool paths и tool-choice evals.

```text
AI Eval Harness.md
```

Добавляет eval fixtures/checks для AI/RAG/OCR/tool behavior, где это можно сделать детерминированно.

## Финальные правила использования

```text
1. Не вставлять весь pack целиком.
2. Не класть manual_prompts в репозиторий как project docs.
3. Для Codex использовать codex code/AGENTS.md.
4. Для Claude Code Cloud использовать claude code/CLAUDE.md.
5. Для каждой задачи вставлять один релевантный prompt-skill.
6. Для нескольких findings сначала запускать Synthesis.md.
7. После meaningful patch запускать Patch Checking.md; он должен проверять весь branch/diff range, а не только последний commit.
8. Для pre-ship запускать Release Readiness Audit.md.
9. Не смешивать standards без repo evidence.
10. Не позволять polish-промпту чинить P2, если в scope остался P0/P1.
```
