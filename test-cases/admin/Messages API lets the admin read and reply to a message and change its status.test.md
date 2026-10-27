<!-- suite
id: @S9b7a1d9b
-->
# Messages API lets the admin read and reply to a message and change its status

<!-- test
id: @Ta02fa522
priority: low
tags: TC-ADM-007, api, admin, REQ-ADM-05, regression
-->
## Messages API lets the admin read and reply to a message and change its status

## Preconditions

- The seed admin account is logged in via `POST /users/login` and has an access token (credentials come from the team secrets and are never written in the case).
- S is a unique suffix for this run (e.g. a timestamp), so names and slugs do not clash with other data.
- A guest message with the subject "QA message S" is sent via `POST /messages` without a token; its `id` is known.

## Steps

1. Send `GET /messages` with the admin token.
*Expected*: The response status is 200 and `data` contains the message with `subject` = "QA message S" and `status` = "NEW".
2. Send `POST /messages/{id}/reply` with `message` = "QA reply S" and the admin token.
*Expected*: The response status is 201 and the body has `message` = "QA reply S".
3. Send `GET /messages/{id}` with the admin token.
*Expected*: The response status is 200, `status` = "IN_PROGRESS", and `replies` contains "QA reply S".
4. Send `PUT /messages/{id}/status` with `status` = "RESOLVED" and the admin token.
*Expected*: The response status is 200 and the body is `{"success": true}`.
5. Send `GET /messages/{id}` with the admin token.
*Expected*: The response status is 200 and `status` = "RESOLVED".
6. Send `PUT /messages/{id}/status` with `status` = "DONE" and the admin token.
*Expected*: The response status is 422 with a `status` error "The selected status is invalid."
