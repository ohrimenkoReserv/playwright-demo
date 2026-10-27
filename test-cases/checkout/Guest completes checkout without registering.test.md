<!-- suite
-->
# Guest completes checkout without registering

<!-- test
priority: critical
tags: TC-CHK-002, e2e, checkout, REQ-CHK-02, regression
-->
## Guest completes checkout without registering

## Preconditions

- A new browser session: no customer is logged in and the cart is empty.
- Product P is ordinary in-stock products (not rentals, not "Thor Hammer", CO2 rating C, D or E), so no cart or invoice discount applies.
- Test data: a guest first name, last name and a unique email.

## Steps

1. Add 1 × P to the cart from its product page, open the cart and click "Proceed to checkout".
*Expected*: The sign-in step offers "Continue as Guest".
2. Enter the guest first name, last name and email and click "Continue as Guest".
*Expected*: The text "Continuing as guest: <first name> <last name> (<email>)" is shown.
3. Click "Proceed to checkout".
*Expected*: The "Billing Address" step is shown.
4. Enter the country, postal code and house number, wait for street, city and state to be filled in, and click "Proceed to checkout".
*Expected*: The "Payment" step is shown.
5. Choose "Cash on Delivery", click "Check payment" and then "Confirm".
*Expected*: The message "Thanks for your order! Your invoice number is …" is shown with an invoice number.
