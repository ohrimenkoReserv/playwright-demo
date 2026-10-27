<!-- suite
id: @Sdda2689d
-->
# Cart content stays after a page reload

<!-- test
id: @T8e7f8a83
priority: low
tags: TC-CART-007, ui, cart, REQ-CART-04, regression
-->
## Cart content stays after a page reload

## Preconditions

- A new browser session: no customer is logged in and the cart is empty.
- Products P and Q are ordinary in-stock products (not rentals, not "Thor Hammer", CO2 rating C, D or E), so no cart or invoice discount applies.
- The cart contains 1 × P and 2 × Q (added from the product pages).

## Steps

1. Open the cart page and reload it.
*Expected*: The cart still has 1 × P and 2 × Q with the same totals, and the cart badge shows 3.
2. Open the home page, reload it, then open the cart again.
*Expected*: The cart is unchanged: 1 × P and 2 × Q.
