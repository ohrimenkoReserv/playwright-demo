<!-- suite
id: @Sefb2c830
-->
# Customer adds a product to favorites and removes it in My favorites

<!-- test
id: @T346e960e
priority: low
tags: TC-FAV-001, ui, favorites, REQ-FAV-01, regression
-->
## Customer adds a product to favorites and removes it in My favorites

## Preconditions

- A new customer account is registered via the API (`POST /users/register`) with a unique email and a unique valid password (the API rejects passwords found in data leaks).
- The customer is logged in via the login form and has no favorites.
- Product P is an ordinary in-stock product (not a rental), its ID is taken from `GET /products`.

## Steps

1. Open the product page of P and click "Add to favorites".
*Expected*: The toast "Product added to your favorites list." is shown.
2. Open "My favorites" from the user menu in the header.
*Expected*: The "Favorites" page lists P with its name and description.
3. Click the delete button of P.
*Expected*: P is no longer listed and the text "There are no favorites yet. In order to add favorites, please go to the product listing and mark some products as your favorite." is shown.
