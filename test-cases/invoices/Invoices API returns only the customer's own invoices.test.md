<!-- suite
-->
# Invoices API returns only the customer's own invoices

<!-- test
priority: normal
tags: TC-INV-002, api, invoices, REQ-INV-01, regression
-->
## Invoices API returns only the customer's own invoices

## Preconditions

- Customers A and B are registered via the API and logged in via `POST /users/login`.
- A and B each have one invoice, created via the API.

## Steps

1. Send `GET /invoices` with A's token.
*Expected*: The response status is 200, `data` contains A's invoice and does not contain B's invoice.
2. Send `GET /invoices/{id}` with A's token and the ID of A's invoice.
*Expected*: The response status is 200 and the body matches the `InvoiceResponse` schema.
