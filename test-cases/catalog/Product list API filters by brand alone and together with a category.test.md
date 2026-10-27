<!-- suite
id: @S5454f8a4
-->
# Product list API filters by brand alone and together with a category

<!-- test
id: @T2c154a7a
priority: normal
tags: TC-CAT-007, api, catalog, REQ-CAT-04, regression
-->
## Product list API filters by brand alone and together with a category

## Preconditions

- The catalog contains the seed data (the database is reset every hour).
- The IDs of the brands "ForgeFlex Tools" and "MightyCraft Hardware" are taken from `GET /brands`.
- The IDs of the subcategories "Pliers" and "Hammer" are taken from `GET /categories/tree`.

## Steps

1. Send `GET /products?by_brand={ForgeFlex Tools ID}` and request every page up to `last_page`.
*Expected*: The response status is 200, `total` is at least 1, and every product has `brand.id` = the ForgeFlex Tools ID.
2. Repeat step 1 with the MightyCraft Hardware ID.
*Expected*: Every product has `brand.id` = the MightyCraft Hardware ID.
3. Send `GET /products?by_brand={brand ID}&by_category={category ID}` for each of the 4 combinations of the two brands and the two categories.
*Expected*: Every response has status 200, every product in it has both the requested `brand.id` and the requested `category.id`, and at least one combination returns products.
