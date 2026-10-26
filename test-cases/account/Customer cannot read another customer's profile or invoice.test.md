<!-- suite
id: @Se42a0fdf
-->
# Customer cannot read another customer's profile or invoice

<!-- test
id: @T6f7c3aea
priority: critical
tags: TC-ACC-004, api, account, REQ-ACC-03, regression
-->
## Customer cannot read another customer's profile or invoice

## Preconditions

- Customers A and B are registered via the API, and both are logged in via `POST /users/login`.
- Customer B has an invoice, created via the API (cart with one product, then `POST /invoices`).

## Steps

1. Send `GET /users/{id}` with A's token and B's user ID.
*Expected*: The response status is 404 and the body has none of B's data (no email, name or address of B).
2. Send `GET /invoices/{id}` with A's token and B's invoice ID.
*Expected*: The response status is 404 and the body has none of the invoice data.
3. Send `GET /invoices/{id}` with B's token and the same invoice ID.
*Expected*: The response status is 200 and the body is the invoice (the ID is valid).
