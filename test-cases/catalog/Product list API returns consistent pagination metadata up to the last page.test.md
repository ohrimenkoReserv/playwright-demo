<!-- suite
id: @S9cfb7fde
-->
# Product list API returns consistent pagination metadata up to the last page

<!-- test
id: @Teacd4838
priority: normal
tags: TC-CAT-001, api, catalog, REQ-CAT-01, regression
-->
## Product list API returns consistent pagination metadata up to the last page

## Preconditions

- The catalog contains the seed data (the database is reset every hour).

## Steps

1. Send `GET /products`.
*Expected*: The response status is 200, `current_page` = 1, `per_page` = 9, `from` = 1, `to` = 9, `data` has 9 products and `last_page` = `total` / 9 rounded up.
2. Send `GET /products?page={last_page}` with `last_page` from step 1.
*Expected*: The response status is 200, `current_page` = `last_page`, `to` = `total`, and `data` has `total` − 9 × (`last_page` − 1) products.
3. Send `GET /products?page={last_page + 1}`.
*Expected*: The response status is 200, `data` is empty, and `from` and `to` are null.
