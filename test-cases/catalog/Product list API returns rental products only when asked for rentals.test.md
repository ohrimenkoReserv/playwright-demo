<!-- suite
id: @Sd7d2b332
-->
# Product list API returns rental products only when asked for rentals

<!-- test
id: @Tfe7f75d9
priority: low
tags: TC-CAT-015, api, catalog, REQ-CAT-09, regression
-->
## Product list API returns rental products only when asked for rentals

## Preconditions

- The catalog contains the seed data (the database is reset every hour).
- The seed data contains rental products (e.g. "Excavator").

## Steps

1. Send `GET /products?is_rental=true`.
*Expected*: The response status is 200, `total` is at least 1, and every product has `is_rental` = true.
2. Send `GET /products` without `is_rental` and request every page up to `last_page`.
*Expected*: No product has `is_rental` = true.
