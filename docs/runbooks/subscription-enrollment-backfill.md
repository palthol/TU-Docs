# Runbook: subscription enrollment backfill

**Audience:** singh  
**Source of truth:** [TU-api `docs/subscription-backfill.md`](https://github.com/palthol/TU-api/blob/develop/docs/subscription-backfill.md) (landed in [TU-api pull request #69](https://github.com/palthol/TU-api/pull/69))  
**This page:** hub pointer + approval gate. Do not copy the long command output from #69.

Enrollment only. It does **not** create charges, billing obligations, or turn on the billing cron.

`--apply` against production needs **singh's explicit OK**. Default is dry-run.

## Why a CLI

A `dry_run` flag on the live HTTP API would be easy to hit by mistake. The CLI runs on a trusted machine with local `services/api/.env`. It calls the same `create_subscription` path as `POST /api/admin/billing/subscriptions` with `create_initial_charge: false`.

## Preconditions

- TU-api checkout that contains #69 (`develop` after that merge).
- `services/api/.env` with **names** `SUPABASE_URL` and `SUPABASE_SECRET_KEY` (or `SUPABASE_SERVICE_ROLE_KEY` if unset). Confirm the printed **hostname** is the host you intend. Scripts print hostname, never keys.
- Do not commit the CSV, result log, or `.env`.
- Do not paste real roster emails or names into this hub, tickets, or chat.

## Steps (summary)

Exact flags and skip/error reasons: [subscription-backfill.md](https://github.com/palthol/TU-api/blob/develop/docs/subscription-backfill.md).

1. **Export** (read-only): `npm --workspace services/api run roster:export -- --out ./tmp/subscription-roster.csv`
2. Fill `plan` (name or id) and `start_date` (`YYYY-MM-DD`, America/New_York). Leave `plan` blank to skip.
3. **Dry-run** (default): `npm --workspace services/api run roster:backfill -- --csv ./tmp/subscription-roster.csv`
4. singh reviews target host, would-create list, skips, errors, implied monthly revenue.
5. **Apply only with OK.** `N` must equal `would_create`:

   ```bash
   npm --workspace services/api run roster:backfill -- --csv ./tmp/subscription-roster.csv --apply --yes-i-reviewed=N
   ```

Without `--apply`, or with a count mismatch, or with row errors, nothing is written. Rerun skips already-enrolled people.

Existing people are enrolled this way. **New walk-ins** (placeholder participants) are a different, **in-progress** flow: [placeholder-enrollment.md](../flows/placeholder-enrollment.md).

## Related HTTP

`POST /api/admin/billing/subscriptions` — one-off enroll in [admin-api.md](https://github.com/palthol/TU-api/blob/develop/docs/admin-api.md). Same RPC; still no cron enablement.
