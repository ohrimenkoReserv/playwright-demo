<!-- suite
id: @S97978a92
-->
# Customer token is rejected on admin endpoints

<!-- test
id: @T4bcbd81b
priority: critical
tags: TC-ACC-005, api, account, REQ-ACC-03, regression, smoke
-->
## Customer token is rejected on admin endpoints

## Preconditions

- A new customer account is registered via the API (`POST /users/register`) with a unique email and a unique valid password (the API rejects passwords found in data leaks).
- The customer is logged in via `POST /users/login` and has an access token.
- The ID of an existing brand is known (`GET /brands`).

## Steps

1. Send `GET /users` with the customer token.
*Expected*: The response status is 403 and the body is `{"message": "Forbidden"}`.
2. Send `DELETE /brands/{id}` with the customer token.
*Expected*: The response status is 403, and `GET /brands/{id}` still returns the brand.
3. Send `GET /reports/total-sales-of-years` with the customer token.
*Expected*: The response status is 403.
