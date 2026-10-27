<!-- suite
id: @S4f01ed93
-->
# Category filter shows only products of the selected categories

<!-- test
id: @T989cc545
priority: normal
tags: TC-CAT-005, ui, catalog, REQ-CAT-03, regression
-->
## Category filter shows only products of the selected categories

## Preconditions

- The catalog contains the seed data (the database is reset every hour).
- The names of the products in the subcategory "Pliers" are taken from `GET /products?by_category_slug=pliers`, and the names of the products in "Hand Tools" and its subcategories from `GET /products?by_category_slug=hand-tools` (all pages).
- A new browser session on the home page.

## Steps

1. In the filters, tick the subcategory "Pliers" under "Hand Tools".
*Expected*: The product list updates and every shown product is one of the "Pliers" products.
2. Untick "Pliers" and tick the parent category "Hand Tools".
*Expected*: All subcategories under "Hand Tools" are ticked, and every shown product is one of the "Hand Tools" products.
