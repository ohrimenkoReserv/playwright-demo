<!-- suite
id: @S64fc5a62
-->
# Product page shows the product details and links to related products

<!-- test
id: @T4c2ae1ba
priority: critical
tags: TC-CAT-012, ui, catalog, REQ-CAT-07, regression, smoke
-->
## Product page shows the product details and links to related products

## Preconditions

- The catalog contains the seed data (the database is reset every hour).
- Product P is an in-stock product with specifications and without a discount (`is_location_offer` = false), e.g. "Combination Pliers"; its name, price, category, brand, description and specs are taken from `GET /products/{id}`.
- At least one other product is in the same category as P.

## Steps

1. Open the product page of P.
*Expected*: The page shows the name, the price, the category and brand badges, the description and a "Specifications" table with the name and value of every spec of P, all equal to the API data.
2. Scroll to "Related products".
*Expected*: The section lists only other products of the same category as P, and P itself is not listed.
3. Click a related product.
*Expected*: The product page of the clicked product opens, with its name in the heading.
