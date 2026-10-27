<!-- suite
id: @S77660058
-->
# Admin marks an order as shipped and the customer sees the new status

<!-- test
id: @Tb46eaf07
priority: normal
tags: TC-ADM-006, e2e, admin, REQ-ADM-04, regression
-->
## Admin marks an order as shipped and the customer sees the new status

## Preconditions

- A new customer account is registered via the API (`POST /users/register`) with a unique email and a unique valid password (the API rejects passwords found in data leaks).
- Product P is an ordinary in-stock product (not a rental, not "Thor Hammer", CO2 rating C, D or E), so no cart or invoice discount applies.
- The customer has one invoice for 1 × P, paid by "Cash on Delivery" and created via the API (`POST /invoices`); its ID and invoice number are known.
- The seed admin account is logged in via the login form (credentials come from the team secrets and are never written in the case).
- A scheduled job moves `AWAITING_FULFILLMENT` orders to `AWAITING_SHIPMENT` and `SHIPPED` orders to `COMPLETED` every 10 minutes, so steps 3–5 are run without a pause.

## Steps

1. Open the admin orders page (`/admin/orders`) and search for the invoice number.
*Expected*: One order with this invoice number is listed, with the status "AWAITING_FULFILLMENT" or "AWAITING_SHIPMENT".
2. Open the order.
*Expected*: The order page shows the invoice number and a status list with the current status.
3. Select "SHIPPED" in the status list and click "Update status".
*Expected*: The message "Status updated!" is shown.
4. Reload the order page.
*Expected*: The status is "SHIPPED", and the earlier statuses can no longer be selected.
5. Send `GET /invoices/{id}` with the customer token.
*Expected*: The response status is 200 and `status` = "SHIPPED".
