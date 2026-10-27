<!-- suite
id: @S32ee3d57
-->
# Messages API accepts a guest message that the admin can read

<!-- test
id: @T44b8dd77
priority: normal
tags: TC-CON-002, api, contact, REQ-CON-01, regression
-->
## Messages API accepts a guest message that the admin can read

## Preconditions

- The seed admin account is logged in via `POST /users/login` and has an access token (credentials come from the team secrets and are never written in the case).
- S is a unique suffix for this run (e.g. a timestamp), so names and slugs do not clash with other data.

## Steps

1. Send `POST /messages` without a token, with `name` = "QA Guest", a unique `email`, `subject` = "QA message S" and a `message` text.
*Expected*: The response status is 200 and the body has the message `id`, `status` = "NEW" and the values sent.
2. Send `GET /messages` with the admin token.
*Expected*: The response status is 200 and `data` contains the message with this `id`.
3. Send `GET /messages/{id}` with the admin token.
*Expected*: The response status is 200 and `name`, `email`, `subject` and `message` equal the values sent.
