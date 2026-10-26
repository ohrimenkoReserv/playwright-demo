<!-- suite
id: @Sd92ce43c
-->
# Register API rejects an email that is already registered

<!-- test
id: @T0b5ba679
priority: normal
tags: TC-AUTH-005, api, auth, REQ-AUTH-03, regression
-->
## Register API rejects an email that is already registered

## Preconditions

- A customer account is registered via the API with email E and password P1.

## Steps

1. Send `POST /users/register` with email E, another first name and another valid password P2.
*Expected*: The response status is 409 and `email` contains "A customer with this email address already exists."
2. Send `POST /users/login` with email E and password P2.
*Expected*: The response status is 401: no second account was created.
3. Send `POST /users/login` with email E and password P1, then `GET /users/me` with the returned token.
*Expected*: Both responses have status 200, and the profile still has the first name of the original account.
