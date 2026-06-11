# README.md Generation

## Mode

- Use the active `AGENTS.md` chain.
- Execute/documentation mode: generate or update the project `README.md` from repository evidence only.

## Goal

Create a useful README that helps a developer understand, run, configure, test, and operate the project without inventing unsupported facts.

## Inspect

Source tree, package/build files, scripts, lockfiles, configs, environment examples, Docker/CI/deploy files, tests, migrations, docs, public assets, route/API definitions, generated artifacts, and existing README content.

## Content rules

- Prefer current repo evidence over stale docs.
- Mention unknowns or missing setup details instead of guessing.
- Keep commands exactly as defined in scripts/configs.
- Include only features, integrations, env vars, routes, deployment steps, and operational notes evidenced in the repo.
- Preserve useful existing README content when still accurate.
- Ground non-obvious repo facts in exact files; use `path:line[-line]` anchors in source notes or final report when useful.
- Write in the repository’s dominant documentation language unless the user requests another language.

## Markdown structure

Use sections that fit the repo and omit irrelevant ones: overview, features, repository structure, prerequisites, installation, configuration/environment variables, local run, commands, architecture/data flow, API/UI routes, testing/validation, deployment/runtime, troubleshooting, and open questions.

Keep the README scannable: one H1, clear H2/H3 groups, compact lists, tables only for dense command/env-var references, and no placeholder sections.

## Validation

After writing, verify the README against inspected scripts/configs and avoid broken commands.

## Final response

Respond in Russian with compact emoji sections: ✅ README changed, 📁 key files, 🔎 key evidence anchors/assumptions, 🧪 checks, ⚠️ unknowns/risks.
