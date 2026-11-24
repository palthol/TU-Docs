# Runbooks

Operator procedures that touch **production** or can destroy data. singh is the only person who may approve those steps.

Gym timezone: America/New_York.

## Software runbooks (this hub)

| Runbook | When |
| --- | --- |
| [Release develop to main](release-develop-to-main.md) | Promote a product repo after CI is green |
| [Apply a migration to production](apply-migration-to-prod.md) | Schema change on the live TU database |
| [Subscription enrollment backfill](subscription-enrollment-backfill.md) | Enroll existing people from a reviewed CSV (TU-api #69) |
| [Resume a paused Supabase project](resume-paused-supabase.md) | API health/deep fails because the DB is paused |

This hub does **not** authorize production writes. Each runbook's apply/deploy step is singh-only.

## Facility SOPs (TU-Operations)

Do not copy cleaning or supply procedures here. Link only:

| SOP | Status | Link |
| --- | --- | --- |
| Mat cleaning and supply budgeting | Open PR, **not** on `main` yet | [TU-Operations PR #14](https://github.com/palthol/TU-Operations/pull/14) · [mat-cleaning-sop.md on `ops/mat-cleaning-standard`](https://github.com/palthol/TU-Operations/blob/ops/mat-cleaning-standard/operations/mat-cleaning-sop.md) |
| Operations workstream | On `main` | [operations/README.md](https://github.com/palthol/TU-Operations/blob/main/operations/README.md) |
| How the ops repo works | On `main` | [TU-Operations README](https://github.com/palthol/TU-Operations/blob/main/README.md) |

Day-to-day gym work is **GitHub Issues** in TU-Operations, not PRs, unless the change *is* a procedure.

## Related software docs (do not treat as runbooks)

- [TU-api current-state.md](https://github.com/palthol/TU-api/blob/develop/docs/current-state.md) — what is verified
- [TU-api deployment.md](https://github.com/palthol/TU-api/blob/develop/docs/deployment.md) — Discord digest cron (Dashboard steps; live job **TODO: verify**)
- [TU-api validation-environment.md](https://github.com/palthol/TU-api/blob/develop/docs/validation-environment.md) — local-only smokes
- [placeholder enrollment flow](../flows/placeholder-enrollment.md) — **in progress** ([TU-api #72](https://github.com/palthol/TU-api/pull/72), [TU-Administrative #18](https://github.com/palthol/TU-Administrative/pull/18); CI blocked by GitHub Actions billing lock)
