<!-- suite
id: @Sad2cb9d9
-->
# Profile API returns the customer's own profile

<!-- test
id: @T77a425c3
priority: normal
tags: TC-ACC-002, api, account, REQ-ACC-01, regression
-->
## Profile API returns the customer's own profile

## Preconditions

- A new customer account is registered via the API (`POST /users/register`) with a unique email and a unique valid password (the API rejects passwords found in data leaks).
- The customer is logged in via `POST /users/login` and has an access token.

## Steps

1. Send `GET /users/me` with the token.
*Expected*: The response status is 200. The body matches the `UserResponse` schema, `email`, `first_name` and `last_name` equal the registration data, and the body has no `password` field.
