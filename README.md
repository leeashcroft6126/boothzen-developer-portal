# BoothZen Developer Portal

Mintlify Git-synced documentation for [developers.boothzen.com](https://developers.boothzen.com).

This repo is the single source of truth for the public BoothZen REST API,
webhooks, SDK, and plugin documentation. It is intentionally separate from the
main application repo so docs can ship on their own cadence and Mintlify can
auto-deploy on every push to `main`.

Part of the BoothZen v14.0 milestone (phase 148).

## What's here

| Path             | Purpose                                                         |
| ---------------- | --------------------------------------------------------------- |
| `docs.json`      | Mintlify site config (theme, navigation, OpenAPI pointer)       |
| `index.mdx`      | Landing page                                                    |
| `logo/`          | Brand logos (light + dark SVGs)                                 |
| `favicon.svg`    | Site favicon                                                    |
| `*.mdx`          | Documentation pages (added by 148-02, 148-03, 148-04)           |

There is intentionally **no static OpenAPI file** in this repo. The
`openapi` field in `docs.json` points to the live spec at
`https://app.boothzen.com/api/v1/openapi.json`, which Scramble emits directly
from the production routes. Mintlify re-fetches on every rebuild, so the
playground never drifts from the live API surface.

## Local preview

```bash
npx mintlify dev
```

Opens a hot-reloading preview at `http://localhost:3000`.

## Adding a page

1. Create the new `.mdx` file at the repo root (or under a subfolder).
2. Add its path (without the `.mdx` extension) to the relevant `pages` array
   in `docs.json` under `navigation.tabs[].groups[].pages`.
3. Commit + push to `main` — Mintlify auto-deploys.

## Git-sync (operator action)

This repo is wired for Mintlify GitHub-app Git-sync. To activate:

1. Install the Mintlify GitHub App on this repo:
   <https://mintlify.com/docs/settings/github>
2. In the Mintlify dashboard, connect the BoothZen project to
   `leeashcroft6126/boothzen-developer-portal` and set `main` as the deploy
   branch.
3. Point the custom domain `developers.boothzen.com` at Mintlify per their DNS
   instructions.

These three steps are surfaced as an operator checkpoint in plan **148-05**.

## Contributing

Open a PR against `main`. Keep page slugs URL-safe and lowercase. Update
`docs.json` navigation when adding pages — Mintlify will not auto-discover.

Contact: [operations@redrawtravel.com](mailto:operations@redrawtravel.com)
