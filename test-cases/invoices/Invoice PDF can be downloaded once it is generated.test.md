<!-- suite
-->
# Invoice PDF can be downloaded once it is generated

<!-- test
priority: low
tags: TC-INV-003, api, invoices, REQ-INV-02, regression
-->
## Invoice PDF can be downloaded once it is generated

## Preconditions

- A new customer account is registered via the API (`POST /users/register`) with a unique email and a unique valid password.
- The customer is logged in via `POST /users/login` and has an access token.
- The customer has an invoice, created via the API, with a known `invoice_number`.

## Steps

1. Send `GET /invoices/{invoice_number}/download-pdf-status` with the token, and repeat while `status` is `IN_PROGRESS`.
*Expected*: The response status is 200 and `status` becomes `COMPLETED`.
2. Send `GET /invoices/{invoice_number}/download-pdf` with the token.
*Expected*: The response status is 200, the `Content-Type` is `application/pdf`, and the body is not empty.
