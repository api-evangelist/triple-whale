---
name: Query Triple Whale analytics with SQL, Moby or the Summary Page
description: >-
  Pull blended performance, attribution and cohort data out of Triple Whale using
  the Data-Out API — custom SQL, natural-language Moby queries, and the Summary
  Page endpoint.
api: openapi/triple-whale-data-out-api-openapi.yml
operations:
  - validate-your-triple-whale-api-key
  - data-out-execute-custom-sql-query
  - data-out-execute-natural-language-query-moby
  - get-summary-page-data
  - get-customer-journey-attribution-data
generated: '2026-08-13'
method: generated
source: >-
  openapi/triple-whale-data-out-api-openapi.yml,
  conventions/triple-whale-conventions.yml,
  errors/triple-whale-problem-types.yml,
  data-model/triple-whale-data-model.yml
---

# Query Triple Whale analytics

Four read paths, and they do not take the same parameters. Pick deliberately.

| Goal | Operation | Shop field |
|---|---|---|
| Arbitrary structured query | `data-out-execute-custom-sql-query` | `shopId` |
| Ask a question in English | `data-out-execute-natural-language-query-moby` | `shopId` |
| Headline blended metrics | `get-summary-page-data` | `shopDomain` |
| Order-level attributed journeys | `get-customer-journey-attribution-data` | `shop` |

## Before you start

- Base URL `https://api.triplewhale.com/api/v2/`, header `x-api-key`.
- Scopes: **Summary Page: Read** for the summary endpoint, **Pixel Attribution:
  Read** for customer journeys. Confirm with
  `validate-your-triple-whale-api-key`.

## Custom SQL

Call `data-out-execute-custom-sql-query` — `POST /orcabase/api/sql`. Required body
fields are `query`, `period.startDate`, `period.endDate` and `shopId`.

- Validate the query in the in-app SQL Builder first.
- **The builder and the API disagree on case.** The builder writes
  `@start_date` / `@end_date`; the API expects `@startDate` / `@endDate` inside the
  SQL string, and `period.startDate` / `period.endDate` in the JSON body. A query
  that runs fine in the builder will 400 from the API for this alone.
- Dates are `YYYY-MM-DD`, and `startDate` must be on or before `endDate`.
- **Never `SELECT *`.** Table schemas are dynamic; column sets shift underneath you.
  Name the columns. Table and metric vocabulary is in the Data Ontology docs and
  mirrored in `data-model/triple-whale-data-model.yml`.

## Natural language (Moby)

Call `data-out-execute-natural-language-query-moby` — `POST /orcabase/api/moby`.
Send the question plus `shopId`. Moby generates SQL and returns grouped JSON
results. Use this for exploratory questions; use SQL when the shape of the answer
must be stable.

## Summary and attribution

- `get-summary-page-data` (`POST /summary-page/get-data`) takes `shopDomain` and a
  period, and returns the Summary Page metrics.
- `get-customer-journey-attribution-data`
  (`POST /attribution/get-orders-with-journeys-v2`) takes `shop` and returns full
  Triple Pixel journeys for every order placed in the period. There is no
  pagination — narrow the date range to bound the response.

## Rules that will bite you

- **A 403 on SQL or Moby almost always means a missing `shopId`,** even though the
  message says `"Access token is required"`. Check the body before you regenerate
  the key. Every other endpoint returns 400 for the same mistake.
- **A 500 usually means the shop identifier does not match a connected store.**
  Check it exactly, then retry once — transient 500s clear in seconds.
- **There is no pagination anywhere.** Chunk by date period instead.
- **Respect `Retry-After` on 429.** Some responses also carry `RateLimit-Policy`
  in `{quota};w={window}` form (e.g. `100;w=60`) and `RateLimit`.
