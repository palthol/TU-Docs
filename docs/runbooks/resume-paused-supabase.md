# Runbook: resume a paused Supabase project

**Audience:** singh  
**TU production ref:** `jhxzecxkccqlgyazhsnb`  
**Symptom:** API process is up (`GET /health` → `{ ok: true }`) but `GET /health/deep` reports `db: false` / unreachable; waivers, admin, and receipts fail.

Supabase can pause a project after inactivity. TU-api docs and operator notes treat this project as **sometimes paused**. Whether it is paused **right now**: **TODO: verify** in the Supabase Dashboard.

Terpsichora is a **different** project. Resuming TU does not resume Terpsichora, and vice versa.

## Preconditions

- You are signed into the Supabase org that owns project `jhxzecxkccqlgyazhsnb`.
- You want the **gym** database, not Terpsichora.
- Resuming is allowed on the project's plan. **TODO: verify** current plan limits (pause/restore behavior) in Dashboard billing.

This runbook does **not** authorize schema changes, data exports, or key rotation.

## Steps (singh)

1. Confirm the API host is Render, not a crashed deploy:
   - `GET https://api.templeunderground.com/health` should be `{ "ok": true }`.
   - `GET https://api.templeunderground.com/health/deep` failing with a DB error points at Supabase, not Express.
2. Open [Supabase Dashboard](https://supabase.com/dashboard) → the TU project (`jhxzecxkccqlgyazhsnb`).
3. If the project shows **Paused**, use Dashboard **Restore** / **Resume** (**TODO: verify** the exact button label in the current Dashboard UI).
4. Wait until the project reports healthy (API URL responds). First resume can take several minutes.
5. Recheck `GET /health/deep` → `{ "ok": true, "db": true }`.
6. Smoke a **read-only** staff action you already use (for example load dashboard People search). Do not run backfill or migrations as part of resume.

## If resume is not the problem

| Check | Why |
| --- | --- |
| Render service suspended / sleep (free web services spin down after inactivity) | API `/health` itself would fail, not only `/health/deep` |
| Wrong `SUPABASE_URL` on Render | Would also fail deep health |
| Terpsichora paused | Technique graph only; gym waiver/admin would still work |

Do not paste restored connection strings or service-role values into git, this hub, or chat.

## Related

- [environments.md](../environments.md)
- [TU-api deployment.md](https://github.com/palthol/TU-api/blob/develop/docs/deployment.md) health table
- Render free-plan spin-down is a **web service** behavior, separate from Supabase pause
