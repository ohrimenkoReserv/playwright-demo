<!-- suite
id: @Sb819951a
-->
# Product list API filters by category

<!-- test
id: @T08b430e1
priority: normal
tags: TC-CAT-006, api, catalog, REQ-CAT-03, regression
-->
## Product list API filters by category

## Preconditions

- The catalog contains the seed data (the database is reset every hour).
- The IDs of all subcategories of "Hand Tools", among them "Pliers" and "Hammer", are taken from `GET /categories/tree`.

## Steps

1. Send `GET /products?by_category={Pliers ID}`.
*Expected*: The response status is 200, `total` is at least 1, and every product in `data` has `category.id` = the Pliers ID.
2. Send `GET /products?by_category={Pliers ID},{Hammer ID}` and request every page up to `last_page`.
*Expected*: Every product has `category.id` equal to the Pliers ID or the Hammer ID, and `total` = the Pliers `total` from step 1 + the `total` of `GET /products?by_category={Hammer ID}`.
3. Send `GET /products?by_category_slug=hand-tools` and request every page up to `last_page`.
*Expected*: The response status is 200, every product has a `category.id` that is one of the "Hand Tools" subcategory IDs, and both Pliers and Hammer products are in the result.
