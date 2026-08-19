---
name: Ingest orders from a custom sales platform into Triple Whale
description: >-
  Push orders, products, customers and subscriptions from a non-native commerce
  platform into Triple Whale using the Data-In API, and safely re-send records to
  correct them.
api: openapi/triple-whale-data-in-api-openapi.yml
operations:
  - validate-your-triple-whale-api-key
  - create-order-record
  - bulk-create-order-records
  - create-customer-record
  - create-product-record
  - create-subscription-record
generated: '2026-08-13'
method: generated
source: >-
  openapi/triple-whale-data-in-api-openapi.yml,
  conventions/triple-whale-conventions.yml,
  errors/triple-whale-problem-types.yml
---

# Ingest orders from a custom sales platform

Use this when the brand's storefront is not one of Triple Whale's native
integrations (Shopify, BigCommerce, WooCommerce) and order data has to be pushed in.

## Before you start

- Base URL is `https://api.triplewhale.com/api/v2/`.
- Authenticate with the `x-api-key` header. Nothing else works — Shopify session
  JWTs are explicitly rejected.
- The key needs the write scopes for the records you are sending: **Orders: Write**,
  **Customers: Write**, **Products: Write**, **Subscriptions: Write**.
- Confirm the key and its scopes first with `validate-your-triple-whale-api-key`
  (`GET /users/api-keys/me`). Do this before the first write, not after a 401.

## Steps

1. **Validate the key.** Call `validate-your-triple-whale-api-key`. If it returns
   401, the key is missing, revoked, or wrong-typed. If the scope you need is not
   in the response, generate a new key with that scope — scopes cannot be added to
   an existing key.

2. **Send customers before orders where you can.** Call `create-customer-record`
   with `shop`, `customer_id`, `platform`, `platform_account_id` plus contact and
   consent fields. This gives orders something to attach to.

3. **Send products.** Call `create-product-record` with `shop`, `product_id`,
   `platform`, `platform_account_id`, and the `variants` / `collections` /
   `images` arrays.

4. **Send orders.** For a single order call `create-order-record`. For a backfill
   call `bulk-create-order-records`, which takes `shop` plus an `orders` array.
   Every order needs `shop`, `order_id`, `platform`, `platform_account_id`,
   `created_at` and `currency`.

5. **Send subscriptions** with `create-subscription-record` if the brand has them;
   the order's `subscription_id` links the two.

## Rules that will bite you

- **The shop field is `shop` on every Data-In endpoint.** It is `shopId` on the SQL
  and Moby endpoints and `shopDomain` on Summary Page. Send it as a plain string —
  `"yourstore.myshopify.com"` — with no slashes and no URL wrapping. A wrong or
  unknown shop returns **500**, not 400.

- **Writes are upserts on a composite natural key, not on `order_id` alone.** To
  update an order, resend it with `shop`, `order_id`, `refund_id`, `created_at`,
  `refunded_at`, `platform` and `platform_account_id` all matching the original.
  Every other field is overwritten with what you send. Change any key field and you
  create a second record instead of updating the first.

- **Retries are safe.** Because of that upsert rule there is no idempotency key and
  none is needed — replaying a failed write with identical key fields converges to
  the same state.

- **A 400 from `bulk-create-order-records` is a partial success.** Valid orders in
  the batch are still processed. Do not replay the whole batch as if nothing
  landed; read which orders failed, fix those, resend them.

- **To delete, void — do not omit.** Resend the record with every field identical
  except `"void": true`. Voided orders and their refunds drop out of all queries.

- **Enrichment endpoints are for native platforms only.** `enrich-orders-data` and
  `enrich-products-data` work for Shopify/BigCommerce/WooCommerce data. For a
  custom sales platform, resend the full record instead.

- **Back off on 429.** Every 429 carries `Retry-After` in seconds. Use exponential
  backoff and space out bulk loops.
