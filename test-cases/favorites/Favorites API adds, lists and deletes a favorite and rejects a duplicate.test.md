<!-- suite
id: @S368592a7
-->
# Favorites API adds, lists and deletes a favorite and rejects a duplicate

<!-- test
id: @T4ef9e4ec
priority: low
tags: TC-FAV-002, api, favorites, REQ-FAV-01, regression
-->
## Favorites API adds, lists and deletes a favorite and rejects a duplicate

## Preconditions

- A new customer account is registered via the API (`POST /users/register`) with a unique email and a unique valid password (the API rejects passwords found in data leaks).
- The customer is logged in via `POST /users/login` and has an access token.
- Product P is an ordinary in-stock product (not a rental), its ID is taken from `GET /products`.

## Steps

1. Send `POST /favorites` with `product_id` = P and the customer token.
*Expected*: The response status is 201 and the body has the favorite `id` and `product_id` = P.
2. Send `GET /favorites` with the customer token.
*Expected*: The response status is 200 and the list has one favorite: the `id` from step 1, with `product_id` = P.
3. Send `POST /favorites` with `product_id` = P again.
*Expected*: The response status is 409 and the body is `{"message": "Duplicate Entry"}`.
4. Send `DELETE /favorites/{id}` with the customer token.
*Expected*: The response status is 204.
5. Send `GET /favorites` with the customer token.
*Expected*: The response status is 200 and the list is empty.
