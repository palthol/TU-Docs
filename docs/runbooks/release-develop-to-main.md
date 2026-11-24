# Runbook: release `develop` to `main`

**Audience:** singh  
**Applies to:** product repos that use `develop` (TU-api, TU-Administrative, Terpsichora). **Not** TU-Docs (this hub PRs straight into `main` and has no `develop`).  
**Does not:** merge, deploy, or rotate keys by itself.

## Rule

Small PRs go into `develop`. CI must pass. singh merges those PRs. A **release** is a later promotion of `develop` → `main`, **only on singh's say-so**.

Production Render/Vercel deploys that follow `main` (or whatever branch the host is set to — **TODO: verify** auto-deploy branch per service) are part of that same gate.

## Preconditions

1. The work you want live is already on `origin/develop`.
2. CI on that `develop` head is green:
   - TU-api: **API tests**, **Detect database changes**, **pgTAP (local Supabase)** when schema changed, **waiver-schema-guard**, **waiver-smoke-test**.
   - TU-Administrative / Terpsichora: that repo's CI. **TODO: verify** required checks on each repo.
3. You have read [TU-api current-state.md](https://github.com/palthol/TU-api/blob/develop/docs/current-state.md) if this release includes API or migrations.
4. If the release **applies schema**, finish [apply-migration-to-prod.md](apply-migration-to-prod.md) **before** or as an explicit paired step. Shipping an API build that selects columns or RPCs that production does not have will break the live API.
5. Billing cron stays **off** unless you separately enable it (not this runbook).

## Steps (singh)

1. Confirm `develop` is the commit you intend (`git log origin/develop -1` on a trusted machine).
2. Open a PR **from `develop` into `main`** on that repo (or merge `develop` → `main` using the GitHub UI). Do not force-push `main`.
3. Wait for the same CI on that PR.
4. Merge **yourself**. Agents and this documentation must not merge.
5. Confirm the host actually deployed:
   - API: `GET https://api.templeunderground.com/health` and `GET /health/deep`
   - Staff apps: load the custom domain (not a Vercel preview)
6. If health/deep fails, check [paused Supabase](resume-paused-supabase.md) before assuming the deploy is bad.

## Rollback (high level)

Redeploy the previous `main` commit on the host, or revert the merge PR. Schema rollbacks are **not** "rerun the old migration." If a migration already applied, restoring schema is a new, explicit migration and needs its own OK. Prefer reverting app code that has not yet required the new columns.

## TU-Docs exception

This repository has only `main` (plus an unrelated `docs/initial-readme` branch that must be left alone). Hub PRs target `main` and are not a gym production deploy.
