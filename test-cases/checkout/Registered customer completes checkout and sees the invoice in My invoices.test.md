<!-- suite
id: @S76122373
-->
# Registered customer completes checkout and sees the invoice in My invoices

<!-- test
id: @Tc1b0cf2f
priority: critical
tags: TC-CHK-001, e2e, checkout, REQ-CHK-01, regression, smoke
-->
## Registered customer completes checkout and sees the invoice in My invoices

## Preconditions

- A new customer account is registered via the API (`POST /users/register`) with a unique email and a unique valid password.
- The customer is logged in via the login form and the cart is empty.
- Products P and Q are ordinary in-stock products (not rentals, not "Thor Hammer", CO2 rating C, D or E), so no cart or invoice discount applies.

## Steps

1. Add 1 × P and 1 × Q to the cart from their product pages.
*Expected*: The cart badge shows 2.
2. Open the cart and click "Proceed to checkout".
*Expected*: The sign-in step says that the customer is already logged in, with the customer's first and last name.
3. Click "Proceed to checkout".
*Expected*: The "Billing Address" step is shown.
4. Enter the country, postal code and house number, wait for street, city and state to be filled in, and click "Proceed to checkout".
*Expected*: The "Payment" step is shown.
5. Choose "Cash on Delivery" and click "Check payment".
*Expected*: The message "Payment was successful" is shown and the button changes to "Confirm".
6. Click "Confirm".
*Expected*: The message "Thanks for your order! Your invoice number is …" is shown with an invoice number.
7. Open "My invoices" (`/account/invoices`).
*Expected*: The list has the invoice with this invoice number and the cart total.
