# AGENTS.md

## Cursor Cloud specific instructions

### Overview

This is the **Contentful Blog Starter Template** — a single Next.js (Pages Router) app that fetches blog content from the Contentful GraphQL API. There is no backend, database, or Docker dependency; the only external requirement is a valid Contentful space with API credentials.

### Required environment variables

The app requires three Contentful secrets in `.env` (see `.env.example`):

- `CONTENTFUL_SPACE_ID`
- `CONTENTFUL_ACCESS_TOKEN`
- `CONTENTFUL_PREVIEW_ACCESS_TOKEN`

Without these, `yarn dev` starts and compiles successfully but every page returns a 404 because `getStaticProps` cannot fetch data. `yarn build` will fail outright.

### Node version

The project pins **Node v18.16.1** (`.nvmrc`). Use `nvm use` to activate it. Yarn (v1 classic) is the package manager — npm is explicitly rejected in `engines`.

### Key commands

| Task | Command |
|------|---------|
| Install deps | `yarn` |
| Dev server | `yarn dev` (port 3000) |
| Lint | `yarn lint` |
| Type-check | `yarn type-check` |
| Build | `yarn build` (requires Contentful credentials) |
| GraphQL codegen | `yarn graphql-codegen:generate` (only when `.graphql` files change) |

### Git hooks (Husky)

Pre-commit and pre-push both run `yarn type-check && yarn lint-staged`. Use `--no-verify` to skip if needed.

### Caveats

- The `next.config.js` emits a warning about `localePath` in `i18n` — this is benign and expected.
- Watchpack may log `EACCES` permission errors for `/etc/credstore`, `/root/.ssh`, etc. in the cloud VM — these are harmless and do not affect functionality.
