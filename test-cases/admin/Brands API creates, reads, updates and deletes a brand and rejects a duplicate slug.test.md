<!-- suite
id: @S7b942c31
-->
# Brands API creates, reads, updates and deletes a brand and rejects a duplicate slug

<!-- test
id: @Tccf99bfa
priority: normal
tags: TC-ADM-001, api, admin, REQ-ADM-01, regression
-->
## Brands API creates, reads, updates and deletes a brand and rejects a duplicate slug

## Preconditions

- The seed admin account is logged in via `POST /users/login` and has an access token (credentials come from the team secrets and are never written in the case).
- S is a unique suffix for this run (e.g. a timestamp), so names and slugs do not clash with other data.

## Steps

1. Send `POST /brands` with `name` = "QA Brand S", `slug` = "qa-brand-s" and the admin token.
*Expected*: The response status is 201 and the body has the brand `id`, `name` = "QA Brand S" and `slug` = "qa-brand-s".
2. Send `GET /brands/{id}`.
*Expected*: The response status is 200 and the body has the same `name` and `slug`.
3. Send `PUT /brands/{id}` with `name` = "QA Brand S updated", `slug` = "qa-brand-s" and the admin token.
*Expected*: The response status is 200, the body is `{"success": true}`, and `GET /brands/{id}` returns the new name.
4. Send `POST /brands` with `name` = "QA Brand S copy", `slug` = "qa-brand-s" and the admin token.
*Expected*: The response status is 422 with a `slug` error "The slug has already been taken."
5. Send `DELETE /brands/{id}` with the admin token.
*Expected*: The response status is 204.
6. Send `GET /brands/{id}`.
*Expected*: The response status is 404 and the body is `{"message": "Requested item not found"}`.
