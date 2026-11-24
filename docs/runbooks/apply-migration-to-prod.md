# Runbook: apply a migration to production

**Audience:** singh  
**Database:** TU Supabase project `jhxzecxkccqlgyazhsnb`  
**Forbidden without singh's explicit OK:** `supabase db push`, Dashboard SQL that changes schema, production data writes, key rotation.

Agents reading this file are **not** authorized to apply anything.

## Why this is gated

Migrations in [TU-api `supabase/migrations/`](https://github.com/palthol/TU-api/tree/develop/supabase/migrations) are the schema source of truth. Applying one changes the **live gym database**. Several files on `develop` are intentionally **in-repo only** (scheduling v2, payer obligations). [current-state.md](https://github.com/palthol/TU-api/blob/develop/docs/current-state.md) lists what production `list_migrations` last showed (audit dated 2026-09-24; **TODO: verify** current applied set before you push).

TU-api scheduling docs call out apply-before-deploy ordering, for example:

- Apply `20261101100500` before an API build that calls `cancel_session`
- Apply `20261101101000` before a build that reads `session_content`
- Apply `20261113175150` before a build that selects `sessions.class_id`
- Apply `20261113190000` before a build that calls booking RPCs or selects `sessions.capacity`

## Preconditions

1. singh has said **yes** for this specific migration filename (or an explicit ordered list).
2. The file is on the git revision you intend to deploy (usually `develop` or the release commit).
3. You have a backup/restore story you accept (Supabase Dashboard → Project Settings → Backups). **TODO: verify** backup retention on this project's plan.
4. Local proof exists: pgTAP / API tests on that revision. CI **Detect database changes** + **pgTAP (local Supabase)** should have run for `supabase/**` PRs.
5. You are **not** paused. If `/health/deep` is down, [resume](resume-paused-supabase.md) first.
6. You will not enable the billing Worker/cron as a side effect of a schema apply.

## Steps (singh)

1. In Supabase Dashboard → Database → Migrations (or `list_migrations` via a trusted, already-authorized operator path), note the last applied version.
2. Confirm the next file(s) to apply match the OK you gave. Do not skip files; order is the filename.
3. Apply with the linked CLI from a trusted machine:

   ```bash
   # From a TU-api checkout at the intended revision
   npm run supabase:push
   ```

   Or run that one SQL file in the Dashboard SQL Editor (service role). Prefer the CLI so history stays consistent.
4. Re-check `list_migrations` / Dashboard that the version appeared.
5. Smoke **read-only** health: `GET https://api.templeunderground.com/health/deep`.
6. Only then deploy the API build that depends on the new RPC/columns ([release runbook](release-develop-to-main.md)).

Do not `db pull` production into git as a way to "fix" history. Do not reuse already-applied version numbers. New files must sort **after** the latest applied name.

## What this runbook is not

- **Enrollment backfill** (`roster:backfill --apply`) — [subscription-enrollment-backfill.md](subscription-enrollment-backfill.md)
- **Reset database** — destroys Auth users and data; not a migration apply
- **Terpsichora** — different project; do not apply TU-api files there

## Related

- [explainer-api-and-db.md](../explainer-api-and-db.md)
- [TU-api AGENTS.md database workflow](https://github.com/palthol/TU-api/blob/develop/AGENTS.md)
- [TU-api use-guide.md](https://github.com/palthol/TU-api/blob/develop/docs/use-guide.md) § 2.3 / 5.1
