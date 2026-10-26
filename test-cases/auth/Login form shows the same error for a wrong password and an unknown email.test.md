<!-- suite
id: @S4a194519
-->
# Login form shows the same error for a wrong password and an unknown email

<!-- test
id: @Tb74e1a6a
priority: critical
tags: TC-AUTH-009, ui, auth, REQ-AUTH-06, regression
-->
## Login form shows the same error for a wrong password and an unknown email

## Preconditions

- A new customer account is registered via the API (`POST /users/register`) with a unique email and a unique valid password (the API rejects passwords found in data leaks).
- The browser has no active session (the customer is not logged in).

## Steps

1. Open the login page (`/auth/login`), enter the customer's email with a wrong password and click "Login".
*Expected*: The error "Invalid email or password" is shown and the login page stays open.
2. Enter an email that is not registered with any password and click "Login".
*Expected*: The same error "Invalid email or password" is shown and the login page stays open.
