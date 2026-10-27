<!-- suite
id: @S6d0cb5c9
-->
# Search API returns only products whose name contains the query

<!-- test
id: @T64501663
priority: critical
tags: TC-CAT-004, api, catalog, REQ-CAT-02, regression, smoke
-->
## Search API returns only products whose name contains the query

## Preconditions

- The catalog contains the seed data (the database is reset every hour).

## Steps

1. Send `GET /products/search?q=pliers`.
*Expected*: The response status is 200, `total` is at least 1, and the name of every product in `data` contains "pliers" (case-insensitive).
2. Send `GET /products/search?q=xyzqwerty`.
*Expected*: The response status is 200, `total` = 0 and `data` is empty.
