<!-- suite
id: @Sea2cd899
-->
# Visitor adds a product with quantity 2 from the product page

<!-- test
id: @T62946717
priority: critical
tags: TC-CART-001, ui, cart, REQ-CART-01, regression, smoke
-->
## Visitor adds a product with quantity 2 from the product page

## Preconditions

- A new browser session: no customer is logged in and the cart is empty.
- Product P is an ordinary in-stock product (not a rental, not "Thor Hammer", CO2 rating C, D or E), so no cart or invoice discount applies.

## Steps

1. Open the product page of P.
*Expected*: The product name, the price and the "Add to cart" button are shown.
2. Increase the quantity to 2.
*Expected*: The quantity field shows 2.
3. Click "Add to cart".
*Expected*: The toast "Product added to shopping cart." is shown and the cart badge in the header shows 2.
4. Open the cart (cart icon in the header).
*Expected*: The cart has one line: P with quantity 2.
