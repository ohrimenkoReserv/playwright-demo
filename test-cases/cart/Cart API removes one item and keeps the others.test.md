<!-- suite
id: @Sc9f92247
-->
# Cart API removes one item and keeps the others

<!-- test
id: @T9944bcd5
priority: normal
tags: TC-CART-006, api, cart, REQ-CART-03, regression
-->
## Cart API removes one item and keeps the others

## Preconditions

- Products P and Q are ordinary in-stock products (not rentals, not "Thor Hammer", CO2 rating C, D or E), so no cart or invoice discount applies.
- A cart is created via the API and contains 1 × P and 2 × Q.

## Steps

1. Send `DELETE /carts/{id}/product/{productId}` with the ID of P.
*Expected*: The response status is 204.
2. Send `GET /carts/{id}`.
*Expected*: `cart_items` has only Q, still with `quantity` = 2.
