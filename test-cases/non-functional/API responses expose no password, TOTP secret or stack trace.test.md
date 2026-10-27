<!-- suite
id: @S907054b7
-->
# API responses expose no password, TOTP secret or stack trace

<!-- test
id: @Tcd4546dc
priority: normal
tags: TC-NFR-006, api, non-functional, REQ-NFR-06, regression
-->
## API responses expose no password, TOTP secret or stack trace

## Preconditions

- The seed admin account is logged in via `POST /users/login` and has an access token (credentials come from the team secrets and are never written in the case).

## Steps

1. Register a new customer via `POST /users/register` with a unique email and a unique valid password.
*Expected*: The response status is 201 and the body has no `password` and no `totp_secret` field.
2. Log in as the customer via `POST /users/login` and send `GET /users/me` with the customer token.
*Expected*: The response status is 200 and the body has no `password` and no `totp_secret` field.
3. Send `GET /users` and `GET /users/{customer id}` with the admin token.
*Expected*: Both responses have status 200, and no user in them has a `password` or `totp_secret` field.
4. Send `GET /products/01AAAAAAAAAAAAAAAAAAAAAAAA`, `GET /no-such-route`, `PATCH /reports/customers-by-country`, `POST /messages` with an empty body, and `GET /messages` without a token.
*Expected*: The responses have status 404, 404, 405, 422 and 401, and each body has only a `message` or field errors and has no `exception`, `trace`, `file` or `line` field and no stack trace text.
