<!-- suite
id: @Sf7574d4b
-->
# Core GET endpoints return responses that match the OpenAPI schemas

<!-- test
id: @Tc21f4b20
priority: normal
tags: TC-NFR-001, api, non-functional, REQ-NFR-01, regression
-->
## Core GET endpoints return responses that match the OpenAPI schemas

## Preconditions

- The OpenAPI spec (v5.0.0) is taken from `https://api.practicesoftwaretesting.com/docs?api-docs.json`. "Matches" means: every property documented in the schema is present with the documented type.
- A new customer account is registered via the API (`POST /users/register`) with a unique email and a unique valid password (the API rejects passwords found in data leaks).
- The customer is logged in via `POST /users/login` and has an access token.
- A product ID and a brand ID are taken from `GET /products` and `GET /brands`.

## Steps

1. Send `GET /products` and `GET /products/search?q=pliers`.
*Expected*: Both responses have status 200 and match `PaginatedProductResponse`, with every item in `data` matching `ProductResponse`.
2. Send `GET /products/{id}`.
*Expected*: The response status is 200 and the body matches `ProductResponse`.
3. Send `GET /brands` and `GET /brands/{id}`.
*Expected*: Both responses have status 200; every item of the list and the single brand match `BrandResponse`.
4. Send `GET /categories/tree`.
*Expected*: The response status is 200 and every item matches `CategoryTreeResponse`.
5. Send `GET /users/me` with the customer token.
*Expected*: The response status is 200 and the body matches `UserResponse`.
6. Send `GET /invoices` with the customer token.
*Expected*: The response status is 200 and the body matches `PaginatedInvoiceResponse`.
