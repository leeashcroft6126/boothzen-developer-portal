# BoothZen Developer Portal

**Live site:** <https://developers.boothzen.com>

[![Link Check](https://github.com/leeashcroft6126/boothzen-developer-portal/actions/workflows/link-check.yml/badge.svg)](https://github.com/leeashcroft6126/boothzen-developer-portal/actions/workflows/link-check.yml)

Mintlify Git-synced documentation for the BoothZen booking platform — REST API,
webhooks, SDKs, and plugins. This repo is the single source of truth and
auto-deploys to `developers.boothzen.com` on every push to `main`.

It is intentionally separate from the main application repo so docs can ship
on their own cadence. Part of the BoothZen v14.0 milestone (phase 148).

## What's here

| Path                          | Purpose                                                         |
| ----------------------------- | --------------------------------------------------------------- |
| `docs.json`                   | Mintlify site config (theme, navigation, live OpenAPI pointer)  |
| `index.mdx`                   | Landing page                                                    |
| `quickstart.mdx`              | First-call walkthrough                                          |
| `authentication.mdx`          | API keys + OAuth                                                |
| `webhooks-reference.mdx`      | 13 observer events + HMAC verification                          |
| `error-codes.mdx`             | Stripe-shape error envelope reference                           |
| `rate-limits.mdx`             | 600/min limit + RateLimit-* headers                             |
| `changelog.mdx`               | Public API + portal changelog                                   |
| `downloads.mdx`               | 5 integration channels (SDK, WP, Joomla, Make, Zapier)          |
| `snippets/`                   | Reusable MDX components (e.g. `manage-api-keys-card.mdx`)       |
| `logo/`                       | Brand logos (light + dark SVGs)                                 |
| `favicon.svg`                 | Site favicon                                                    |
| `public/`                     | Static files served at root (llms.txt, sitemap.xml, robots.txt) |
| `.github/workflows/link-check.yml` | Lychee CI on push + PR + weekly cron                       |

There is intentionally **no static OpenAPI file** in this repo. The `openapi`
field in `docs.json` points to the live spec at
`https://app.boothzen.com/api/v1/openapi.json`, which Scramble emits directly
from the production routes. Mintlify re-fetches on every rebuild, so the
playground never drifts from the live API surface.

## Local preview

```bash
npx mintlify dev
```

Opens a hot-reloading preview at <http://localhost:3000>.

## Mintlify Git-sync setup (operator action)

This repo is wired for Mintlify GitHub-app Git-sync. Activation is a one-time
operator action — surfaced as an operator checkpoint in plan **148-05**.

1. **Install the Mintlify GitHub App.** Open
   <https://github.com/apps/mintlify/installations/new> in a browser logged in
   as `leeashcroft6126`. Choose **Only select repositories** →
   `boothzen-developer-portal` → **Install**.
2. **Connect the repo in the Mintlify dashboard.** Sign in at
   <https://dashboard.mintlify.com> with GitHub, click **Connect repo**, select
   `leeashcroft6126/boothzen-developer-portal`, choose `main` as the deploy
   branch, save. The first build will trigger automatically.
3. **Add the custom domain.** In the Mintlify dashboard's **Domains** section,
   click **Add custom domain**, enter `developers.boothzen.com`, and copy the
   CNAME target Mintlify provides (e.g. `cname.mintlify.app`).
4. **Add the Cloudflare CNAME.** In Cloudflare DNS for `boothzen.com`, add:
   - Type: `CNAME`
   - Name: `developers`
   - Target: *(the CNAME target from step 3)*
   - Proxy status: **DNS only** (grey cloud — orange cloud breaks Mintlify's
     Let's Encrypt TLS issuance)
   - TTL: Auto

   Wait ~5 minutes; the Mintlify dashboard will flip the domain status from
   Pending → Active and issue TLS automatically.

## Contributing

Open a PR against `main`. Keep page slugs URL-safe and lowercase. Update
`docs.json` navigation when adding pages — Mintlify will not auto-discover.

Contact: [operations@redrawtravel.com](mailto:operations@redrawtravel.com)

## License

MIT — see [LICENSE](LICENSE). This portal follows the SDK/Zapier/Make
ecosystem norm (MIT), distinct from the WP plugin / Joomla module GPL norm.
