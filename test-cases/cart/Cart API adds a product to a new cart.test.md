<!-- suite
id: @S2c9a204a
-->
# Cart API adds a product to a new cart

<!-- test
id: @Tdb80f33a
priority: critical
tags: TC-CART-002, api, cart, REQ-CART-01, regression, smoke
-->
## Cart API adds a product to a new cart

## Preconditions

- Product P is an ordinary in-stock product (not a rental, not "Thor Hammer", CO2 rating C, D or E), so no cart or invoice discount applies.

## Steps

1. Send `POST /carts`.
*Expected*: The response status is 201 and the body has the cart `id`.
2. Send `POST /carts/{id}` with `product_id` = P and `quantity` = 2.
*Expected*: The response status is 200 and the body is `{"result": "item added or updated"}`.
3. Send `GET /carts/{id}`.
*Expected*: The response status is 200 and `cart_items` has one item with `product_id` = P and `quantity` = 2.
