<!-- suite
id: @Sc94796a2
-->
# Admin adds a product that is shown and found in the shop

<!-- test
id: @T92046a20
priority: normal
tags: TC-ADM-005, ui, admin, REQ-ADM-03, regression
-->
## Admin adds a product that is shown and found in the shop

## Preconditions

- The seed admin account is logged in via the login form (credentials come from the team secrets and are never written in the case).
- S is a unique suffix of digits for this run (e.g. a timestamp). The product name "QAProductS" is one word, so the shop search finds it.

## Steps

1. Open the admin products page (`/admin/products`) and click "Add Product".
*Expected*: The page "Add Product" is shown.
2. Enter the name "QAProductS", a description, stock 10 and price 19.99, select a brand, a category and an image, and click "Save".
*Expected*: The message "Product saved!" is shown.
3. Open the shop home page and search for "QAProductS".
*Expected*: The result has the product card "QAProductS" with the price $19.99.
4. Open the product card.
*Expected*: The product page shows the name "QAProductS", the price $19.99 and the selected category and brand.
