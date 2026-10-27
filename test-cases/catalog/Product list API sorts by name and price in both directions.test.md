<!-- suite
id: @S5ae5406f
-->
# Product list API sorts by name and price in both directions

<!-- test
id: @Tdf5276be
priority: normal
tags: TC-CAT-011, api, catalog, REQ-CAT-06, regression
-->
## Product list API sorts by name and price in both directions

## Preconditions

- The catalog contains the seed data (the database is reset every hour).

## Steps

1. Send `GET /products?sort=name,asc` and `GET /products?sort=name,asc&page=2`.
*Expected*: Both responses have status 200, and the names on pages 1 and 2 together are in ascending order (case-insensitive).
2. Repeat step 1 with `sort=name,desc`.
*Expected*: The names on pages 1 and 2 together are in descending order (case-insensitive).
3. Repeat step 1 with `sort=price,asc`.
*Expected*: The prices on pages 1 and 2 together are in ascending order.
4. Repeat step 1 with `sort=price,desc`.
*Expected*: The prices on pages 1 and 2 together are in descending order, and the first price is the highest price of all products.
