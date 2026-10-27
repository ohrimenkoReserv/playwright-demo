<!-- suite
-->
# Payment check accepts all five payment methods with valid details

<!-- test
priority: critical
tags: TC-CHK-005, api, checkout, REQ-CHK-04, regression, smoke
-->
## Payment check accepts all five payment methods with valid details

## Preconditions

- No access token is needed.

## Steps

1. Send `POST /payment/check` with `payment_method` = `bank-transfer` and `payment_details` `bank_name` = "Test Bank", `account_name` = "Jane Doe", `account_number` = "123456789".
*Expected*: The response status is 200 and the body is `{"message": "Payment was successful"}`.
2. Send `POST /payment/check` with `payment_method` = `cash-on-delivery` and empty `payment_details`.
*Expected*: The response status is 200 and the body is `{"message": "Payment was successful"}`.
3. Send `POST /payment/check` with `payment_method` = `credit-card` and `payment_details` `credit_card_number` = "1111-2222-3333-4444", `expiration_date` = a month in the future as MM/YYYY, `cvv` = "123", `card_holder_name` = "Jane Doe".
*Expected*: The response status is 200 and the body is `{"message": "Payment was successful"}`.
4. Send `POST /payment/check` with `payment_method` = `buy-now-pay-later` and `payment_details` `monthly_installments` = 3.
*Expected*: The response status is 200 and the body is `{"message": "Payment was successful"}`.
5. Send `POST /payment/check` with `payment_method` = `gift-card` and `payment_details` `gift_card_number` = "ABCD1234EFGH5678", `validation_code` = "AB12".
*Expected*: The response status is 200 and the body is `{"message": "Payment was successful"}`.
