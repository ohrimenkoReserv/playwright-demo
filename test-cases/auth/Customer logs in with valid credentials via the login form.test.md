<!-- suite
id: @S3497cbcd
-->
# Customer logs in with valid credentials via the login form

<!-- test
id: @Ta8031e0b
priority: critical
tags: TC-AUTH-007, ui, auth, REQ-AUTH-05, regression, smoke
-->
## Customer logs in with valid credentials via the login form

## Preconditions

- A new customer account is registered via the API (`POST /users/register`) with a unique
  email, a valid password and a first and last name.
- The browser has no active session (the customer is not logged in).

## Steps

1. Open the login page (`/auth/login`).
*Expected*: The login form with email and password fields is displayed.
2. Enter the customer's email and password.
3. Click "Login".
*Expected*: The customer is redirected to the account page (`/account`) with the heading "My account", and the header shows the customer's first and last name instead of the "Sign in" link.
