<!-- suite
id: @S5ec3bc39
-->
# Forgot password API gives the same response for known and unknown emails

<!-- test
id: @T20efd27d
priority: low
tags: TC-AUTH-015, api, auth, REQ-AUTH-10, regression
-->
## Forgot password API gives the same response for known and unknown emails

## Preconditions

- A new customer account is registered via the API (`POST /users/register`) with a unique email and a unique valid password (the API rejects passwords found in data leaks). Use only this account: a password reset changes its password.

## Steps

1. Send `POST /users/forgot-password` with the customer's email.
*Expected*: The response status is 200.
2. Send `POST /users/forgot-password` with an email that is not registered.
*Expected*: The response status and body are identical to step 1, so the response does not reveal whether the email is registered.
