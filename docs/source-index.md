# Source index

Links to key docs in each Temple Underground repo. Prefer these over copying long sections into this hub.

Branch used when a repo has `develop`: **`develop`**. Otherwise the default branch. Retrieved 2026-11-24.

## This hub (TU-Docs)

| Doc | Path |
| --- | --- |
| Hub home | [README.md](../README.md) |
| API/DB explainer | [docs/explainer-api-and-db.md](explainer-api-and-db.md) |
| System map | [docs/system-map.md](system-map.md) |
| Data model | [docs/data-model.md](data-model.md) |
| Environments | [docs/environments.md](environments.md) |
| Runbooks | [docs/runbooks/](runbooks/README.md) |
| Placeholder enrollment | [docs/flows/placeholder-enrollment.md](flows/placeholder-enrollment.md) |

`docs/initial-readme` is a **git branch**, not a folder. Leave it alone.

## [TU-api](https://github.com/palthol/TU-api) (`develop`)

The main software source of truth.

| Doc | URL |
| --- | --- |
| README | https://github.com/palthol/TU-api/blob/develop/README.md |
| Agent / repo guide | https://github.com/palthol/TU-api/blob/develop/AGENTS.md |
| Docs index | https://github.com/palthol/TU-api/blob/develop/docs/README.md |
| Current state | https://github.com/palthol/TU-api/blob/develop/docs/current-state.md |
| Admin API contracts | https://github.com/palthol/TU-api/blob/develop/docs/admin-api.md |
| Database overview | https://github.com/palthol/TU-api/blob/develop/docs/database-overview.md |
| Scheduling v2 | https://github.com/palthol/TU-api/blob/develop/docs/scheduling/README.md |
| Subscription backfill | https://github.com/palthol/TU-api/blob/develop/docs/subscription-backfill.md |
| Deployment / env names | https://github.com/palthol/TU-api/blob/develop/docs/deployment.md |
| Validation env | https://github.com/palthol/TU-api/blob/develop/docs/validation-environment.md |
| Ownership / data flow | https://github.com/palthol/TU-api/blob/develop/docs/application-ownership-and-data-flow.md |
| Use guide | https://github.com/palthol/TU-api/blob/develop/docs/use-guide.md |
| Target state | https://github.com/palthol/TU-api/blob/develop/docs/target-state.md |
| Schema audit | https://github.com/palthol/TU-api/blob/develop/docs/api-schema-audit.md |
| Recurring obligations | https://github.com/palthol/TU-api/blob/develop/docs/recurring-billing-obligations.md |
| Migrations | https://github.com/palthol/TU-api/tree/develop/supabase/migrations |
| Env example (names) | https://github.com/palthol/TU-api/blob/develop/services/api/.env.example |
| CI | https://github.com/palthol/TU-api/blob/develop/.github/workflows/ci.yml |
| Waiver guards | https://github.com/palthol/TU-api/blob/develop/.github/workflows/waiver-guards.yml |
| Enrollment CLI PR | https://github.com/palthol/TU-api/pull/69 |
| Placeholder participants PR (open, into `develop`) | https://github.com/palthol/TU-api/pull/72 |
| Billing cron worker (off) | https://github.com/palthol/TU-api/blob/develop/workers/billing-cron/README.md |

## [TU-Administrative](https://github.com/palthol/TU-Administrative) (`develop`)

Staff apps. No backend.

| Doc | URL |
| --- | --- |
| README | https://github.com/palthol/TU-Administrative/blob/develop/README.md |
| Agent guide | https://github.com/palthol/TU-Administrative/blob/develop/AGENTS.md |
| Front-end design index | https://github.com/palthol/TU-Administrative/blob/develop/docs/frontend-design/README.md |
| API reference (admin clients) | https://github.com/palthol/TU-Administrative/blob/develop/docs/frontend-design/api-reference.md |
| Dashboard redesign / gates | https://github.com/palthol/TU-Administrative/blob/develop/docs/frontend-design/dashboard-redesign.md |
| Receipts map | https://github.com/palthol/TU-Administrative/blob/develop/docs/frontend-design/receipts-app.md |
| Waiver viewer map | https://github.com/palthol/TU-Administrative/blob/develop/docs/frontend-design/waiver-viewer.md |
| Dashboard env names | https://github.com/palthol/TU-Administrative/blob/develop/apps/dashboard/.env.example |
| Enrollment board PR (open, into `develop`) | https://github.com/palthol/TU-Administrative/pull/18 |

Domains: `admin.templeunderground.com`, `finance.templeunderground.com`, `waiverviewer.templeunderground.com`.

## [TU-Signup](https://github.com/palthol/TU-Signup) (`main`)

Public waiver wizard. Calls TU-api waiver routes.

| Doc | URL |
| --- | --- |
| README | https://github.com/palthol/TU-Signup/blob/main/README.md |
| Submit payload | https://github.com/palthol/TU-Signup/blob/main/docs/frontend-backend-payload.md |

## [Terpsichora](https://github.com/palthol/Terpsichora) (`develop`)

Separate visual-learning app and **separate** Supabase project. No classes or calendar.

| Doc | URL |
| --- | --- |
| README | https://github.com/palthol/Terpsichora/blob/develop/README.md |
| Architecture | https://github.com/palthol/Terpsichora/blob/develop/docs/ARCHITECTURE.md |
| Admin / editor | https://github.com/palthol/Terpsichora/blob/develop/docs/ADMIN_EDITOR.md |
| Env names | https://github.com/palthol/Terpsichora/blob/develop/.env.example |
| Migrations | https://github.com/palthol/Terpsichora/tree/develop/supabase/migrations |
| Deployed app | https://terpsichora.vercel.app |

Default git branch is `master`; `develop` is the integration branch used here.

## [TU-Operations](https://github.com/palthol/TU-Operations) (`main`)

Operator docs and SOPs. GitHub Issues are the work backlog.

| Doc | URL |
| --- | --- |
| README | https://github.com/palthol/TU-Operations/blob/main/README.md |
| Vision | https://github.com/palthol/TU-Operations/blob/main/docs/vision.md |
| Operating standards | https://github.com/palthol/TU-Operations/blob/main/docs/operating-standards.md |
| Prioritization | https://github.com/palthol/TU-Operations/blob/main/docs/prioritization.md |
| Facility notes | https://github.com/palthol/TU-Operations/blob/main/docs/facility.md |
| Operations workstream | https://github.com/palthol/TU-Operations/blob/main/operations/README.md |
| Mat cleaning SOP | Not on `main`. [PR #14](https://github.com/palthol/TU-Operations/pull/14) · [file on branch](https://github.com/palthol/TU-Operations/blob/ops/mat-cleaning-standard/operations/mat-cleaning-sop.md) |

## Mentioned siblings (not read in full for this hub)

TU-api `AGENTS.md` also names marketing repos (`TU-web`, `TU-marketing`). They are not part of this hub's required sources. **TODO: verify** whether they should be added later.

## Could not verify

See [environments.md](environments.md) for remaining `TODO: verify` items (Terpsichora hosted project ref, Render auto-deploy branch, current pause state, Signup custom domain, dashboard/signup local port overlap).

Placeholder enrollment PRs (open into `develop`, not merged; GitHub Actions billing lock so CI has not run): [TU-api #72](https://github.com/palthol/TU-api/pull/72), [TU-Administrative #18](https://github.com/palthol/TU-Administrative/pull/18).
