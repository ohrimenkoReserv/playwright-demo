<!-- suite
id: @S4a0ca92c
-->
# Register API rejects passwords that break a password rule

<!-- test
id: @Ta715b62b
priority: normal
tags: TC-AUTH-003, api, auth, REQ-AUTH-02, regression
-->
## Register API rejects passwords that break a password rule

## Preconditions

- Each request uses a new unique email and otherwise valid registration data.
- Passwords are unique (not found in data leaks), so only the rule under test fails.

## Steps

1. Send `POST /users/register` with a 7-character password that has upper and lower case letters, a number and a symbol.
*Expected*: The response status is 422 and `password` contains "The password field must be at least 8 characters."
2. Send `POST /users/register` with an 8-character password that has upper and lower case letters, a number and a symbol.
*Expected*: The response status is 201.
3. Send `POST /users/register` with a password without upper case letters.
*Expected*: The response status is 422 and `password` contains "The password field must contain at least one uppercase and one lowercase letter."
4. Send `POST /users/register` with a password without lower case letters.
*Expected*: The response status is 422 and `password` contains "The password field must contain at least one uppercase and one lowercase letter."
5. Send `POST /users/register` with a password without a number.
*Expected*: The response status is 422 and `password` contains "The password field must contain at least one number."
6. Send `POST /users/register` with a password without a symbol.
*Expected*: The response status is 422 and `password` contains "The password field must contain at least one symbol."
