<!-- suite
id: @S6db920b3
-->
# Removing an item in the cart updates the total and the badge

<!-- test
id: @Tdf180112
priority: normal
tags: TC-CART-005, ui, cart, REQ-CART-03, regression
-->
## Removing an item in the cart updates the total and the badge

## Preconditions

- A new browser session: no customer is logged in and the cart is empty.
- Products P and Q are ordinary in-stock products (not rentals, not "Thor Hammer", CO2 rating C, D or E), so no cart or invoice discount applies.
- The cart contains 1 × P and 2 × Q (added from the product pages) and the cart page is open.

## Steps

1. Click the remove button of P.
*Expected*: The line of P disappears, the line of Q stays with quantity 2, the cart total equals the line total of Q, and the cart badge shows 2.
