# TU-Docs

Central documentation hub for **Temple Underground** (TU), a boxing and BJJ gym.

The goal is to maintain clear, consistent, and version-controlled documentation for gym operations, software, environments, and administrative processes.

This repository is the map: how the pieces fit together, which environment is which, and which runbooks need singh's explicit OK. Facility SOPs (mat cleaning, supply budgeting, and other physical operations) live in [TU-Operations](https://github.com/palthol/TU-Operations) — this hub links to them rather than copying them.

singh is the sole staff member, admin, and operator. The gym's business timezone is **America/New_York**.

## What this hub is

Product code, schema, and app-specific docs stay in their own repos.

| This hub | Sibling repos |
| --- | --- |
| Cross-repo architecture, environments, and operator runbooks | API contracts, schema, app screens, and facility SOPs |

## Navigation

| Doc | Use it for |
| --- | --- |
| [docs/explainer-api-and-db.md](docs/explainer-api-and-db.md) | Plain-language picture of the API and database (for a non-specialist owner) |
| [docs/system-map.md](docs/system-map.md) | Apps, API, Supabase projects, hosting, and domains |
| [docs/data-model.md](docs/data-model.md) | Main entities and relationships by domain |
| [docs/environments.md](docs/environments.md) | Local, develop, and production; config **names** only |
| [docs/runbooks/](docs/runbooks/README.md) | Releases, production migrations, enrollment backfill, paused Supabase |
| [docs/flows/placeholder-enrollment.md](docs/flows/placeholder-enrollment.md) | Placeholder participants and enrollment (**in progress**) |
| [docs/source-index.md](docs/source-index.md) | Links to every repo's key docs |

## Repos at a glance

| Repo | Role |
| --- | --- |
| [TU-api](https://github.com/palthol/TU-api) | Express API + TU Supabase schema (source of truth for gym data) |
| [TU-Administrative](https://github.com/palthol/TU-Administrative) | Staff apps: dashboard, receipts, waiver viewer |
| [TU-Signup](https://github.com/palthol/TU-Signup) | Public signup and waiver app |
| [Terpsichora](https://github.com/palthol/Terpsichora) | Visual technique-learning app (separate Supabase project) |
| [TU-Operations](https://github.com/palthol/TU-Operations) | Operator docs and SOPs |
| This repo (`TU-Docs`) | Central hub |

## Conventions

- **Link, don't copy.** Summarize here and point at the owning repo's docs.
- **No secrets.** Never commit keys, tokens, connection strings, webhook URLs, or real member/athlete data (no names, emails, dates of birth, or counts tied to people). Project refs and public hostnames already in the repos are fine.
- **Names only for config.** Environment variable **names** belong here; values do not.
- **Unverified facts** are marked `TODO: verify` instead of guessed.
- **Timezone.** Wall-clock class times, late-cancel windows, and enrollment dates use America/New_York unless a doc says otherwise.
- **Approval gates.** Production migrations, deploys, key rotation, and production data writes need **singh's explicit OK**. Do not apply, deploy, or `--apply` from this documentation.
- **Links.** Relative paths inside this repo; full `https://github.com/palthol/...` URLs for other repos.

## How work is released (product repos)

This is the workflow used by TU-api, TU-Administrative, and sibling product repos. **TU-Docs itself has no `develop` branch** — hub changes PR into `main`.

1. Small PRs into `develop`.
2. CI must pass.
3. singh merges.
4. Releases go `develop` → `main` only on singh's say-so.

See [docs/runbooks/release-develop-to-main.md](docs/runbooks/release-develop-to-main.md).

## Roadmap (software)

1. **Admin ops first** — waivers, people, families, money and payments, invoices.
2. **Scheduling** — class catalog, per-session notes and videos, staff booking (**in progress** on TU-api `develop`).
3. **Member-facing apps** — a future member portal; Terpsichora is expected to share login with that portal later.

Placeholder participants and enrollment (walk-ins who can book before signing the new waiver) are a current in-progress slice: [TU-api #72](https://github.com/palthol/TU-api/pull/72) and [TU-Administrative #18](https://github.com/palthol/TU-Administrative/pull/18) (both into `develop`, not merged; GitHub Actions billing lock so CI has not run). See [docs/flows/placeholder-enrollment.md](docs/flows/placeholder-enrollment.md).
