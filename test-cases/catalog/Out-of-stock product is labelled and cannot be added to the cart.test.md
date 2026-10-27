<!-- suite
id: @S36323c01
-->
# Out-of-stock product is labelled and cannot be added to the cart

<!-- test
id: @Tddd48519
priority: normal
tags: TC-CAT-014, ui, catalog, REQ-CAT-08, regression
-->
## Out-of-stock product is labelled and cannot be added to the cart

## Preconditions

- The catalog contains the seed data (the database is reset every hour).
- Product O is out of stock (`in_stock` = false in `GET /products/{id}`), e.g. "Long Nose Pliers" in the seed data.
- A new browser session with an empty cart.

## Steps

1. Search for O by name on the home page.
*Expected*: The product card of O shows "Out of stock".
2. Open the product page of O.
*Expected*: The text "Out of stock" is shown, and the "Add to cart" button, the quantity field and the quantity buttons are disabled.
