<!-- suite
id: @Se7773ac5
-->
# Token refresh returns a new working token

<!-- test
id: @T5a456b2c
priority: low
tags: TC-AUTH-014, api, auth, REQ-AUTH-09, regression
-->
## Token refresh returns a new working token

## Preconditions

- A new customer account is registered via the API (`POST /users/register`) with a unique email and a unique valid password (the API rejects passwords found in data leaks).
- The customer is logged in via `POST /users/login` and has access token A.

## Steps

1. Send `GET /users/refresh` with token A.
*Expected*: The response status is 200. The body has `access_token` B (a JWT different from A), `token_type` equal to `bearer` (case-insensitive) and a positive number `expires_in`.
2. Send `GET /users/me` with token B.
*Expected*: The response status is 200 and the body is the customer's profile.
