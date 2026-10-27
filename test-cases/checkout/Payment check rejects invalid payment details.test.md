<!-- suite
id: @S5d98b065
-->
# Payment check rejects invalid payment details

<!-- test
id: @Td45ad254
priority: critical
tags: TC-CHK-007, api, checkout, REQ-CHK-05, regression
-->
## Payment check rejects invalid payment details

## Preconditions

- No access token is needed.
- Each request is otherwise valid: only the field under test is invalid.

## Steps

1. Send `POST /payment/check` with `payment_method` = `credit-card` and `credit_card_number` = "1111222233334444" (no dashes).
*Expected*: The response status is 422 with an error for `payment_details.credit_card_number`.
2. Send `POST /payment/check` with `payment_method` = `credit-card` and an `expiration_date` in the past (e.g. "01/2020").
*Expected*: The response status is 422 with an error for `payment_details.expiration_date`.
3. Send `POST /payment/check` with `payment_method` = `credit-card` and `cvv` = "12".
*Expected*: The response status is 422 with an error for `payment_details.cvv`.
4. Send `POST /payment/check` with `payment_method` = `gift-card` and no `validation_code`.
*Expected*: The response status is 422 with an error for `payment_details.validation_code`.
