<!-- suite
-->
# Changing the quantity in the cart recalculates line and cart totals

<!-- test
priority: critical
tags: TC-CART-003, ui, cart, REQ-CART-02, regression
-->
## Changing the quantity in the cart recalculates line and cart totals

## Preconditions

- A new browser session: no customer is logged in and the cart is empty.
- Product P is ordinary in-stock products (not rentals, not "Thor Hammer", CO2 rating C, D or E), so no cart or invoice discount applies.
- The cart contains 1 × P (added from the product page) and the cart page is open.

## Steps

1. Change the quantity of P from 1 to 3.
*Expected*: The line total of P equals its unit price × 3, and the cart total equals this line total.
