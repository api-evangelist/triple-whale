---
name: Send offline pixel events and handle PII deletion requests
description: >-
  Close customer-journey gaps by sending server-side and offline Triple Pixel
  events, and honour customer data-deletion requests through the Compliance API.
api: openapi/triple-whale-data-in-api-openapi.yml
operations:
  - validate-your-triple-whale-api-key
  - enrich-pixel-with-offline-events
  - create-pps-record
  - create-compliance-request
generated: '2026-08-13'
method: generated
source: >-
  openapi/triple-whale-data-in-api-openapi.yml,
  openapi/triple-whale-compliance-api-openapi.yml,
  conventions/triple-whale-conventions.yml,
  errors/triple-whale-problem-types.yml
---

# Offline pixel events and PII deletion

Two unrelated jobs that share one thing: both write to a customer's identity graph,
so both need care.

## Offline and server-side pixel events

`enrich-pixel-with-offline-events` — `POST /data-in/event`. Use it for leads, MQLs,
SQLs, opportunities, book-a-demo events, and fully custom events that never touch
the browser.

Body fields: `shop`, `type`, `profileIdentifiers`, `eventId`, `timestamp`,
`event_name`, `source`, and optionally `campaign` / `adset` / `ad`.

- `profileIdentifiers` is what joins the event back into the pixel identity graph.
  Without it the event lands but attributes to nothing.
- When `type` is `custom` you may add properties of type Number, Float, String,
  Boolean or Date.
- **Hard limits: 1,000 events per minute and 3 KB per event.** Exceeding the size
  returns **413 Payload Too Large**; exceeding the rate returns **429** with
  `Retry-After`. Trim custom properties before you batch harder.
- `eventId` is your dedupe handle — reuse it on a retry so the same real-world
  event does not land twice.

## Post-purchase survey responses

`create-pps-record` — `POST /data-in/pps`. Requires `shop`, `platform`,
`platform_account_id`, `order_id`, `created_at`, `question_id`, `question_text`,
`response_id`, `response`, and `include_in_attribution`.

- This is the one Data-In endpoint that returns **404**: `Order Not Found`. Send the
  order through `create-order-record` first, then the survey response.
- Set `include_in_attribution` deliberately — it decides whether the response feeds
  the attribution model or is reporting-only.

## Deletion and masking requests

`create-compliance-request` — `POST /compliance/requests/create-request`. Needs the
**Compliance: Write** scope.

- Submit one or more identifiers (emails and/or phone numbers) for a shop; Triple
  Whale deletes or masks the matching customer PII.
- A **403 Forbidden** here means the key lacks the Compliance: Write scope.
- Treat this as irreversible. Confirm the identifier set before sending; there is no
  undo operation in the published API.
- The docs publish a sample Python automation for submitting deletion requests from
  a CSV — use that shape for bulk right-to-be-forgotten work rather than a tight
  loop, and honour `Retry-After` on 429.
