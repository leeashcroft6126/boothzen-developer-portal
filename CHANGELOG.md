# Changelog

All notable changes to the BoothZen developer portal are documented here.
Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/). This repo uses Semantic Versioning.

## [0.1.0] — 2026-05-11

### Added
- Initial Mintlify site scaffold at /home/ubuntu/boothzen-developer-portal with docs.json pointing to the live OpenAPI spec at https://app.boothzen.com/api/v1/openapi.json (no static spec drift).
- Content pages: Quickstart, Authentication, Webhooks Reference, Error Codes, Rate Limits, Changelog, Downloads.
- Downloads page linking to Laravel SDK (Packagist), WordPress plugin (.zip), Joomla module (.zip), Make.com module (.zip), and Zapier private-beta invite.
- Reusable `manage-api-keys-card.mdx` snippet deep-linking to https://app.boothzen.com/admin/settings/api-keys (PORTAL-06 single source of truth).
- Lychee link-check CI on push + PR + weekly cron.
- llms.txt + llms-full.txt (llmstxt.org-compliant) for AI crawler discovery.
- sitemap.xml + robots.txt for traditional search crawlers.
- OpenGraph + Twitter meta defaults in docs.json.
- Custom subdomain developer.boothzen.com via Cloudflare CNAME → Mintlify.

[0.1.0]: https://github.com/leeashcroft6126/boothzen-developer-portal/releases/tag/v0.1.0
