# Triple Whale (triple-whale)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
