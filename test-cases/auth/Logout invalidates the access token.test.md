<!-- suite
id: @S2df6fd40
-->
# Logout invalidates the access token

<!-- test
id: @T37bce7f8
priority: normal
tags: TC-AUTH-012, api, auth, REQ-AUTH-08, regression
-->
## Logout invalidates the access token

## Preconditions

- A new customer account is registered via the API (`POST /users/register`) with a unique email and a unique valid password (the API rejects passwords found in data leaks).
- The customer is logged in via `POST /users/login` and has an access token.

## Steps

1. Send `GET /users/me` with the token.
*Expected*: The response status is 200.
2. Send `GET /users/logout` with the token.
*Expected*: The response status is 200 and the body is `{"message": "Successfully logged out"}`.
3. Send `GET /users/me` with the same token.
*Expected*: The response status is 401.
