<!-- suite
id: @Sb6e1217a
-->
# Signing out in the UI blocks access to the account pages

<!-- test
id: @T37bc5137
priority: normal
tags: TC-AUTH-013, ui, auth, REQ-AUTH-08, regression
-->
## Signing out in the UI blocks access to the account pages

## Preconditions

- A new customer account is registered via the API (`POST /users/register`) with a unique email and a unique valid password (the API rejects passwords found in data leaks).
- The customer is logged in via the login form and the account page (`/account`) is open.

## Steps

1. Open the user menu in the header and click "Sign out".
*Expected*: The header shows the "Sign in" link instead of the customer's name.
2. Open the account page (`/account`) by its URL.
*Expected*: The login page (`/auth/login`) is displayed instead of the account page.
