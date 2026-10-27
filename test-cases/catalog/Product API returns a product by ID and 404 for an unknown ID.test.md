<!-- suite
id: @Sc312b3bc
-->
# Product API returns a product by ID and 404 for an unknown ID

<!-- test
id: @T585c692f
priority: critical
tags: TC-CAT-013, api, catalog, REQ-CAT-07, regression, smoke
-->
## Product API returns a product by ID and 404 for an unknown ID

## Preconditions

- The catalog contains the seed data (the database is reset every hour).
- Product P is an ordinary in-stock product (not a rental), its ID is taken from `GET /products`.

## Steps

1. Send `GET /products/{P}`.
*Expected*: The response status is 200, `id` = P, and the body matches the `ProductResponse` schema of the OpenAPI spec: `name`, `description`, `price`, `is_location_offer`, `is_rental`, `in_stock`, `co2_rating`, `is_eco_friendly`, `brand`, `category` and `product_image`.
2. Send `GET /products/01AAAAAAAAAAAAAAAAAAAAAAAA` (a valid ID that does not exist).
*Expected*: The response status is 404 and the body is `{"message": "Requested item not found"}`.
