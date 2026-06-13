# Triple Whale (triple-whale)

Triple Whale is an e-commerce analytics and attribution platform built for Shopify brands and DTC merchants. It provides a two-way data highway through its Data-In and Data-Out REST APIs, enabling brands to push external data into the platform and query pixel attribution, cohort analytics, creative metrics, blended ROAS, and summary dashboard metrics. Authentication supports both OAuth2 (for third-party integrations) and personal API keys. The platform integrates with 60+ tools including TikTok, Shopify, Klaviyo, QuickBooks, Google BigQuery, AWS Redshift, and Snowflake.

APIs.json: [https://raw.githubusercontent.com/api-evangelist/triple-whale/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/triple-whale/refs/heads/main/apis.yml)

Naftiko: [https://github.com/naftiko/fleet?utm_source=api-evangelist&utm_medium=readme&utm_campaign=triple-whale-api-evangelist&utm_content=repo](https://github.com/naftiko/fleet?utm_source=api-evangelist&utm_medium=readme&utm_campaign=triple-whale-api-evangelist&utm_content=repo)

## Tags

- E-commerce
- Analytics
- Attribution
- Shopify
- Pixel Tracking
- ROAS
- DTC
- Marketing

## APIs

### Triple Whale Summary API

Data-Out API for retrieving dashboard summary page metrics for specified timeframes, giving brands access to centralized metrics from 60+ integrated tools.

### Triple Whale Attribution API

Data-Out API for querying customer journey attribution data powered by Triple Whale's proprietary pixel-tracking technology, with support for exporting to data warehouses.

### Triple Whale Data-In API

Ingestion API for pushing external data into Triple Whale, including ad records, orders, customers, products, subscriptions, post-purchase survey responses, and offline pixel events.

## Plans, Rate Limits, and FinOps

- **Plans/Pricing**: [plans/triple-whale-plans-pricing.yml](plans/triple-whale-plans-pricing.yml) — Four tiers: Free ($0), Foundation ($219/mo+), Automate ($749/mo+), Enterprise (custom). Pricing scales with GMV.
- **Rate Limits**: [rate-limits/triple-whale-rate-limits.yml](rate-limits/triple-whale-rate-limits.yml) — Offline events capped at 1,000/minute; 3 KB max payload per event. OAuth2 and API key auth supported.
- **FinOps**: [finops/triple-whale-finops.yml](finops/triple-whale-finops.yml) — FOCUS-aligned cost allocation by plan tier, GMV bracket, and add-on modules.

## Timestamps

- Created: 2026-06-13
- Modified: 2026-06-13

## Common

| Type | URL |
|------|-----|
| Website | https://www.triplewhale.com |
| Documentation | https://triplewhale.readme.io/reference/introduction-to-the-triple-whale-api |
| GitHub Org | https://github.com/Triple-Whale |
| LinkedIn | https://www.linkedin.com/company/triple-whale |
| Blog | https://www.triplewhale.com/blog |
| Pricing | https://www.triplewhale.com/pricing |
| Status Page | https://status.triplewhale.com |
| X | https://x.com/triplewhale |

## Maintainers

- Kin Lane (kin@apievangelist.com)
