<!-- suite
-->
# Invoice total equals the sum of its line totals

<!-- test
priority: critical
tags: TC-CHK-008, api, checkout, REQ-CHK-06, regression
-->
## Invoice total equals the sum of its line totals

## Preconditions

- A new customer account is registered via the API (`POST /users/register`) with a unique email and a unique valid password.
- The customer is logged in via `POST /users/login` and has an access token.
- Products P and Q are ordinary in-stock products (not rentals, not "Thor Hammer", CO2 rating C, D or E), so no cart or invoice discount applies.
- A cart is created via the API and contains 2 × P and 3 × Q.
- Billing address: a country and a postal code valid for it, with `street`, `city` and `state` taken from `GET /postcode-lookup` for that country and postal code (the API rejects a city or state that does not belong to the postal code).

## Steps

1. Send `POST /invoices` with the token, the billing address, `payment_method` = `cash-on-delivery`, `payment_details` = `{}` and the `cart_id`.
*Expected*: The response status is 201 and the body has the invoice `id`.
2. Send `GET /invoices/{id}` with the token.
*Expected*: The invoice has two lines: P with `quantity` = 2 and Q with `quantity` = 3, each `unit_price` equal to the product price. `subtotal` equals Σ(`quantity` × `unit_price`), the discount amounts are 0, and `total` equals `subtotal`.
