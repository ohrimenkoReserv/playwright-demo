<!-- suite
id: @Sebf802ed
-->
# Login API returns the same error for a wrong password and an unknown email

<!-- test
id: @T739ce77d
priority: critical
tags: TC-AUTH-010, api, auth, REQ-AUTH-06, regression
-->
## Login API returns the same error for a wrong password and an unknown email

## Preconditions

- A new customer account is registered via the API (`POST /users/register`) with a unique email and a unique valid password (the API rejects passwords found in data leaks).

## Steps

1. Send `POST /users/login` with the customer's email and a wrong password.
*Expected*: The response status is 401 and the body is `{"error": "Unauthorized"}`.
2. Send `POST /users/login` with an email that is not registered.
*Expected*: The response status is 401 and the body is identical to the body in step 1.
