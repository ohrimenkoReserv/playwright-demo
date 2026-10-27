<!-- suite
id: @S501316bc
-->
# Shopper uses the menu, search and cart on a mobile viewport

<!-- test
id: @T2263de21
priority: low
tags: TC-NFR-005, ui, non-functional, REQ-NFR-05, regression
-->
## Shopper uses the menu, search and cart on a mobile viewport

## Preconditions

- The browser emulates a Pixel 7 (viewport 412 × 915, touch).
- Product P is an ordinary in-stock product (not a rental), its ID is taken from `GET /products`.
- A new browser session with an empty cart.

## Steps

1. Open the home page.
*Expected*: The navigation is collapsed into the menu button, and the page has no horizontal scrolling.
2. Tap the menu button.
*Expected*: The menu shows "Home", "Categories", "Contact" and "Sign in".
3. Tap "Filters" on the home page and search for the name of P.
*Expected*: The filter panel opens with the search field, and the result shows the product card of P.
4. Open P and tap "Add to cart".
*Expected*: The toast "Product added to shopping cart." is shown.
5. Open the menu and tap the cart icon.
*Expected*: The cart page shows P with quantity 1.
