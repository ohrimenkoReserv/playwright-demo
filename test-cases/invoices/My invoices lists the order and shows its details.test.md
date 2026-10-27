<!-- suite
-->
# My invoices lists the order and shows its details

<!-- test
priority: normal
tags: TC-INV-001, ui, invoices, REQ-INV-01, regression
-->
## My invoices lists the order and shows its details

## Preconditions

- A new customer account is registered via the API (`POST /users/register`) with a unique email and a unique valid password.
- Product P is ordinary in-stock products (not rentals, not "Thor Hammer", CO2 rating C, D or E), so no cart or invoice discount applies.
- The customer has one invoice for 1 × P, paid by "Cash on Delivery" (created via the API or a checkout).
- The customer is logged in via the login form.

## Steps

1. Open "My invoices" (`/account/invoices`).
*Expected*: The list has the invoice with its invoice number, invoice date and total.
2. Open the details of the invoice.
*Expected*: The details show the invoice number, the billing address, the payment method "Cash on Delivery", and the product line P with quantity 1, its price and the total.
