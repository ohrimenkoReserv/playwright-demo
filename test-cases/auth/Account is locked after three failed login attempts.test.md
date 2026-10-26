<!-- suite
id: @Sc4d5e5b4
-->
# Account is locked after three failed login attempts

<!-- test
id: @Tcae5b22a
priority: normal
tags: TC-AUTH-011, api, auth, REQ-AUTH-07, regression
-->
## Account is locked after three failed login attempts

## Preconditions

- A new customer account is registered via the API (`POST /users/register`) with a unique email and a unique valid password (the API rejects passwords found in data leaks).

## Steps

1. Send `POST /users/login` with the customer's email and a wrong password three times.
*Expected*: Each response has status 401.
2. Send `POST /users/login` with the customer's email and the correct password.
*Expected*: The response status is 423, the body is `{"error": "Account locked, too many failed attempts. Please contact the administrator."}`, and no `access_token` is returned.
