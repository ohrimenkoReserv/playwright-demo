<!-- suite
id: @S7f844192
-->
# Messages API rejects missing fields, a guest without an email and a too long message

<!-- test
id: @T98189bf0
priority: normal
tags: TC-CON-004, api, contact, REQ-CON-02, regression
-->
## Messages API rejects missing fields, a guest without an email and a too long message

## Preconditions

- No `Authorization` header is sent in any step (guest).
- A valid body has `name` = "QA Guest", a unique `email`, `subject` = "QA validation" and a `message` text.

## Steps

1. Send `POST /messages` with the valid body without `subject`.
*Expected*: The response status is 422 with a `subject` error "The subject field is required."
2. Send `POST /messages` with the valid body without `message`.
*Expected*: The response status is 422 with a `message` error "The message field is required."
3. Send `POST /messages` with the valid body without `email`.
*Expected*: The response status is 422 with an `email` error.
4. Send `POST /messages` with the valid body and a `message` of 251 characters.
*Expected*: The response status is 422 with a `message` error "The message field must not be greater than 250 characters."
5. Send `POST /messages` with the valid body and a `message` of exactly 250 characters.
*Expected*: The response status is 200 and the body has `status` = "NEW".
