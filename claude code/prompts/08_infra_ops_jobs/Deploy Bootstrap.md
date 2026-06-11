# Deploy Bootstrap — Minimal CI/CD and Infra

## Mode

- Use the active `CLAUDE.md` context if present, then repository evidence.
- Work in the current Claude Code Cloud session. Do not assume hidden background runs or extra delegation mechanisms unless the user explicitly provides them.
- Implementation mode: create a minimal production-usable deployment setup when repo evidence supports it.

## Goal

Implement a simple CI/CD path where a pull-request update validates the repo and a commit to `main` deploys exactly the triggering `github.sha` to a Linux server over SSH, using Docker Compose v2, host Nginx, health checks, safe cleanup after successful deploy, and a first-run runbook in `infra/README.md`.

## Target defaults

### Server and traffic

- Server user: `root`.
- Server path: `/root/$PROJECT_DIR`, with `PROJECT_DIR` inferred from the repository name unless repo/user evidence says otherwise.
- Public traffic: Cloudflare → host Nginx → Dockerized app.
- Published app ports bind to `127.0.0.1`; host Nginx is the public entry point.

### GitHub Actions

- CI runs on pull request create/update/reopen/ready-for-review, not ordinary branch pushes.
- CD runs only on `push` to `main`; do not also deploy on `pull_request.closed`.
- Deploy the exact `github.sha`, not the latest branch head.
- Use GitHub Secrets for sensitive values and Variables for non-sensitive environment-specific values.
- Required Secret: `DEPLOY_SSH_PRIVATE_KEY`.
- Optional Secret: `APP_ENV_FILE`.
- Required Variables: `DEPLOY_HOST`, `DEPLOY_PATH`, `DOMAIN_NAME`.
- Optional Variables when needed: `DEPLOY_SSH_PORT`, `APP_PORT`, `WEB_PORT`, `HEALTHCHECK_PATH`, `MIGRATION_COMMAND`.
- Because the default deployment user is fixed to `root`, do not introduce `SSH_USER`/`DEPLOY_USER` unless the project explicitly needs it.

## Deliverables

Create or update only the files needed for the detected stack. Usually this includes:

- `.github/workflows/ci.yml`
- `.github/workflows/cd.yml`
- `docker-compose.yml`
- `scripts/deploy.sh`
- `scripts/cleanup-docker.sh`
- `infra/nginx.conf.template`
- `infra/README.md`
- `Dockerfile` only when framework/build/start/port can be detected safely

Do not create optional registry, scaling, Cloudflare API automation, logrotate, multi-environment, replicas, blue/green deploy, or observability machinery unless repository evidence or the user request requires it.

## Detection first

Inspect and report the actual package manager, framework, start/build/test/lint/typecheck commands, Docker/Compose status, migrations, workers, health endpoint, runtime env vars, ports, service topology, and assumptions/placeholders.

If a command or runtime fact cannot be detected, do not invent it. Add a safe placeholder or documented manual step only where that keeps the setup honest.

## Deployment invariants

- Remote deploy script fetches from origin and checks out/resets to `DEPLOY_COMMIT` exactly.
- Missing `DEPLOY_COMMIT` fails deploy; no branch-head fallback.
- `.env`/`APP_ENV_FILE` is written without printing secrets and with restrictive permissions.
- Add worker services only when the repo has a worker/background process; workers do not publish ports.
- Migrations, if detected, run as forward-only deploy steps unless the repo has a rollback plan.
- Nginx config is rendered for `DOMAIN_NAME`; run `nginx -t` before reload.
- Cleanup runs only after health verification succeeds.
- Existing unrelated Nginx, Docker, workflow, or deploy files are preserved unless intentionally replaced for this setup.

## Validation

Run relevant repo-native checks plus workflow syntax sanity where possible, Docker build/config checks when Docker is present or created, shell syntax checks for scripts, and config rendering sanity for Nginx. Document checks that cannot run in Claude Code Cloud.

## Final response

Respond in Russian with compact emoji sections: ✅ deployment setup, 📁 files changed, 🔎 detected stack/evidence anchors, 🔐 required secrets/variables, 🧪 validation, 🧭 first manual server steps, ⚠️ assumptions/placeholders/risks, ⛔ not run/not included.
