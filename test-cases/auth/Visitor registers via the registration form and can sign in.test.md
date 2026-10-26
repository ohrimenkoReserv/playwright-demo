<!-- suite
id: @Sb9052dde
-->
# Visitor registers via the registration form and can sign in

<!-- test
id: @T53f8a73d
priority: critical
tags: TC-AUTH-001, ui, auth, REQ-AUTH-01, regression
-->
## Visitor registers via the registration form and can sign in

## Preconditions

- The browser has no active session (the customer is not logged in).
- Test data: a unique email and a unique valid password (at least 8 characters with upper and lower case letters, a number and a symbol).

## Steps

1. Open the registration page (`/auth/register`).
*Expected*: The "Customer registration" form is displayed.
2. Fill in all fields with valid data: first and last name, date of birth (age between 18 and 75), country, postal code valid for that country, house number, street, city, state, phone (digits only), email and password.
3. Click "Register".
*Expected*: The login page (`/auth/login`) is displayed.
4. Log in with the new email and password.
*Expected*: The account page (`/account`) is displayed and the header shows the first and last name entered at registration.
