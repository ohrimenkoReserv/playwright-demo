<!-- suite
id: @Sa25be6f8
-->
# Billing address step cannot be completed with empty required fields

<!-- test
id: @Te0299e9e
priority: normal
tags: TC-CHK-004, ui, checkout, REQ-CHK-03, regression
-->
## Billing address step cannot be completed with empty required fields

## Preconditions

- A new browser session: no customer is logged in and the cart is empty.
- Product P is an ordinary in-stock product (not a rental, not "Thor Hammer", CO2 rating C, D or E), so no cart or invoice discount applies.
- The cart contains 1 × P, the guest details are entered on the sign-in step, and the "Billing Address" step is open.

## Steps

1. Leave all address fields empty.
*Expected*: The "Proceed to checkout" button is disabled.
2. Enter the country, postal code and house number, wait for street, city and state to be filled in, then clear the street and the city.
*Expected*: The street and city fields are marked as invalid and the "Proceed to checkout" button is disabled.
3. Enter the street and the city again.
*Expected*: No field is marked as invalid and the "Proceed to checkout" button is enabled.
