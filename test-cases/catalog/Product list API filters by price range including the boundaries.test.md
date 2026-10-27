<!-- suite
id: @Sddd2d921
-->
# Product list API filters by price range including the boundaries

<!-- test
id: @Te00a10c1
priority: low
tags: TC-CAT-009, api, catalog, REQ-CAT-05, regression
-->
## Product list API filters by price range including the boundaries

## Preconditions

- The catalog contains the seed data (the database is reset every hour).
- Two products A and B with prices min < max and at least one other product priced between them are taken from `GET /products` (e.g. 12.01 and 14.24 in the seed data).

## Steps

1. Send `GET /products?between=price,{min},{max}` and request every page up to `last_page`.
*Expected*: The response status is 200, every product has min ≤ `price` ≤ max, and A and B are both in the result.
2. Send `GET /products?between=price,{max},{max}`.
*Expected*: The response status is 200 and every product in `data` has `price` = max, B included.
