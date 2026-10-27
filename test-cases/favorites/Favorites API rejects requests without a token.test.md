<!-- suite
id: @S9b4ff51a
-->
# Favorites API rejects requests without a token

<!-- test
id: @Te0bc1eb8
priority: low
tags: TC-FAV-003, api, favorites, REQ-FAV-02, regression
-->
## Favorites API rejects requests without a token

## Preconditions

- Product P is an ordinary in-stock product (not a rental), its ID is taken from `GET /products`.

## Steps

1. Send `POST /favorites` with `product_id` = P and no `Authorization` header.
*Expected*: The response status is 401 and the body is `{"message": "Unauthorized"}`.
2. Send `GET /favorites` without a token.
*Expected*: The response status is 401 and the body is `{"message": "Unauthorized"}`.
3. Send `DELETE /favorites/01AAAAAAAAAAAAAAAAAAAAAAAA` without a token.
*Expected*: The response status is 401 and the body is `{"message": "Unauthorized"}`.
