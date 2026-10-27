<!-- suite
id: @S84b2c269
-->
# Catalog write requests without a token are rejected

<!-- test
id: @Tc9debbcd
priority: critical
tags: TC-ADM-010, api, admin, REQ-ADM-08, regression, smoke
-->
## Catalog write requests without a token are rejected

## Preconditions

- `01AAAAAAAAAAAAAAAAAAAAAAAA` is a valid ID that does not exist, so no data can change even if a request is not protected.
- No `Authorization` header is sent in any step.

## Steps

1. Send `DELETE /brands/01AAAAAAAAAAAAAAAAAAAAAAAA`.
*Expected*: The response status is 401 and the body is `{"message": "Unauthorized"}`.
2. Send `DELETE /categories/01AAAAAAAAAAAAAAAAAAAAAAAA`.
*Expected*: The response status is 401 and the body is `{"message": "Unauthorized"}`.
3. Send `DELETE /products/01AAAAAAAAAAAAAAAAAAAAAAAA`.
*Expected*: The response status is 401 and the body is `{"message": "Unauthorized"}`.
4. Send `POST /brands` with an empty body.
*Expected*: The response status is 401.
5. Send `PUT /brands/01AAAAAAAAAAAAAAAAAAAAAAAA` with an empty body.
*Expected*: The response status is 401.
6. Send `PATCH /brands/01AAAAAAAAAAAAAAAAAAAAAAAA` with an empty body.
*Expected*: The response status is 401.
