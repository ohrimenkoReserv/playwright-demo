<!-- suite
id: @S888a1ce1
-->
# Customer changes the password and only the new one works

<!-- test
id: @T4376640c
priority: normal
tags: TC-ACC-003, api, account, REQ-ACC-02, regression
-->
## Customer changes the password and only the new one works

## Preconditions

- A new customer account is registered via the API (`POST /users/register`) with a unique email and a unique valid password (the API rejects passwords found in data leaks). Its password is P1.
- The customer is logged in via `POST /users/login` and has an access token.
- Test data: a new unique valid password P2.

## Steps

1. Send `POST /users/change-password` with the token and `current_password` = P1, `new_password` = P2, `new_password_confirmation` = P2.
*Expected*: The response status is 200 and the body is `{"success": true}`.
2. Send `POST /users/login` with the customer's email and P1.
*Expected*: The response status is 401.
3. Send `POST /users/login` with the customer's email and P2.
*Expected*: The response status is 200 and the body has an `access_token`.
