<!-- suite
id: @S02d7d8df
-->
# Registration form shows password rule errors and blocks submit

<!-- test
id: @T0117f349
priority: normal
tags: TC-AUTH-004, ui, auth, REQ-AUTH-02, regression
-->
## Registration form shows password rule errors and blocks submit

## Preconditions

- The browser has no active session (the customer is not logged in).
- Test data: valid registration data with a unique email.

## Steps

1. Open the registration page (`/auth/register`).
*Expected*: The form shows the password rules: at least 8 characters, upper and lower case letters, at least one number, at least one special symbol.
2. Fill in all fields except the password with valid data.
3. Enter a 7-character password with upper and lower case letters, a number and a symbol.
*Expected*: The rule "Be at least 8 characters long" is not marked as met; the other three rules are marked as met.
4. Click "Register".
*Expected*: A password error says that the password must be at least 8 characters long, and the registration page stays open.
5. Replace the password with an 8-character password without upper case letters and click "Register".
*Expected*: The rule "Contain both uppercase and lowercase letters" is not marked as met, a password error is shown, and the registration page stays open.
6. Try to log in with the entered email and the last password.
*Expected*: The login is rejected: no account was created.
