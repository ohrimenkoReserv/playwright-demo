<!-- suite
-->
# Cart API updates the quantity of a cart item

<!-- test
priority: critical
tags: TC-CART-004, api, cart, REQ-CART-02, regression
-->
## Cart API updates the quantity of a cart item

## Preconditions

- Product P is ordinary in-stock products (not rentals, not "Thor Hammer", CO2 rating C, D or E), so no cart or invoice discount applies.
- A cart is created via the API (`POST /carts`) and contains 1 × P.

## Steps

1. Send `PUT /carts/{id}/product/quantity` with `product_id` = P and `quantity` = 3.
*Expected*: The response status is 200 and the body is `{"result": "item added or updated"}`.
2. Send `GET /carts/{id}`.
*Expected*: The item P has `quantity` = 3 and an unchanged `product.price`, so its line total is `product.price` × 3.
