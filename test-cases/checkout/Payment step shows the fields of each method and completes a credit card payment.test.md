<!-- suite
id: @Sc9ad9e12
-->
# Payment step shows the fields of each method and completes a credit card payment

<!-- test
id: @Tc6e6858b
priority: critical
tags: TC-CHK-006, ui, checkout, REQ-CHK-04, regression
-->
## Payment step shows the fields of each method and completes a credit card payment

## Preconditions

- A new browser session: no customer is logged in and the cart is empty.
- Product P is an ordinary in-stock product (not a rental, not "Thor Hammer", CO2 rating C, D or E), so no cart or invoice discount applies.
- The cart contains 1 × P, the guest details and the billing address are entered, and the "Payment" step is open.

## Steps

1. Choose "Bank Transfer".
*Expected*: The fields Bank Name, Account Name and Account Number are shown.
2. Choose "Cash on Delivery".
*Expected*: No payment detail fields are shown.
3. Choose "Buy Now Pay Later".
*Expected*: A monthly installments selector is shown.
4. Choose "Gift Card".
*Expected*: The fields gift card number and validation code are shown.
5. Choose "Credit Card".
*Expected*: The fields credit card number, expiration date, CVV and card holder name are shown.
6. Enter credit card number "1111-2222-3333-4444", an expiration date in the future, CVV "123" and card holder name "Jane Doe", and click "Check payment".
*Expected*: The message "Payment was successful" is shown and the button changes to "Confirm".
7. Click "Confirm".
*Expected*: The message "Thanks for your order! Your invoice number is …" is shown with an invoice number.
