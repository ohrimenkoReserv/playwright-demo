<!-- suite
-->
# Guest invoice API creates an invoice for valid data and rejects invalid data

<!-- test
priority: critical
tags: TC-CHK-003, api, checkout, REQ-CHK-02, regression
-->
## Guest invoice API creates an invoice for valid data and rejects invalid data

## Preconditions

- Product P is ordinary in-stock products (not rentals, not "Thor Hammer", CO2 rating C, D or E), so no cart or invoice discount applies.
- Each request uses its own cart, created via the API with 1 × P.
- Billing address: a country and a postal code valid for it, with `street`, `city` and `state` taken from `GET /postcode-lookup` for that country and postal code (the API rejects a city or state that does not belong to the postal code).
- No access token is sent.

## Steps

1. Send `POST /invoices/guest` with the billing address, `payment_method` = `cash-on-delivery`, `payment_details` = `{}`, `cart_id`, `guest_email`, `guest_first_name` and `guest_last_name`.
*Expected*: The response status is 201 and the body has an `invoice_number` and a `total` equal to the price of P.
2. Send the same request without `guest_email`.
*Expected*: The response status is 422 with a `guest_email` error "The guest email field is required."
3. Send the same request with `guest_email` = `not-an-email`.
*Expected*: The response status is 422 with a `guest_email` error "The guest email field must be a valid email address."
