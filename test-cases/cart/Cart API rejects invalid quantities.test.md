<!-- suite
id: @Sb72715b7
-->
# Cart API rejects invalid quantities

<!-- test
id: @T70309b1e
priority: normal
tags: TC-CART-008, api, cart, REQ-CART-05, regression
-->
## Cart API rejects invalid quantities

## Preconditions

- Product P is an ordinary in-stock product (not a rental, not "Thor Hammer", CO2 rating C, D or E), so no cart or invoice discount applies.
- A cart is created via the API and contains 1 × P.

## Steps

1. Send `POST /carts/{id}` with `product_id` = P and `quantity` = 0.
*Expected*: The response status is 422 with a `quantity` error "The quantity field must be at least 1."
2. Send the same request with `quantity` = -1.
*Expected*: The response status is 422 with a `quantity` error "The quantity field must be at least 1."
3. Send the same request with `quantity` = "abc".
*Expected*: The response status is 422 with a `quantity` error "The quantity field must be an integer."
4. Send the same request with `quantity` = 100.
*Expected*: The response status is 422 with a `quantity` error "The quantity field must not be greater than 99."
5. Send `GET /carts/{id}`.
*Expected*: The cart is unchanged: P with `quantity` = 1.
