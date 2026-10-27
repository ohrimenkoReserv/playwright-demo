<!-- suite
id: @Se329d2c1
-->
# Categories API manages a parent and a child category and updates the category tree

<!-- test
id: @Tcf6577a6
priority: low
tags: TC-ADM-003, api, admin, REQ-ADM-02, regression
-->
## Categories API manages a parent and a child category and updates the category tree

## Preconditions

- The seed admin account is logged in via `POST /users/login` and has an access token (credentials come from the team secrets and are never written in the case).
- S is a unique suffix for this run (e.g. a timestamp), so names and slugs do not clash with other data.

## Steps

1. Send `POST /categories` with `name` = "QA Parent S", `slug` = "qa-parent-s" and the admin token.
*Expected*: The response status is 201 and the body has the parent `id`.
2. Send `POST /categories` with `name` = "QA Child S", `slug` = "qa-child-s", `parent_id` = the parent ID and the admin token.
*Expected*: The response status is 201 and the body has the child `id` and `parent_id` = the parent ID.
3. Send `GET /categories/tree`.
*Expected*: The response status is 200 and the tree has "QA Parent S" with "QA Child S" in its `sub_categories`.
4. Send `PUT /categories/{child id}` with `name` = "QA Child S updated" and the admin token.
*Expected*: The response status is 200, the body is `{"success": true}`, and `GET /categories/tree` shows "QA Child S updated" under "QA Parent S".
5. Send `POST /categories` with `name` = "QA Parent S copy", `slug` = "qa-parent-s" and the admin token.
*Expected*: The response status is 422 with a `slug` error "The slug has already been taken."
6. Send `DELETE /categories/{child id}` and then `DELETE /categories/{parent id}` with the admin token.
*Expected*: Both responses have status 204, and `GET /categories/tree` contains neither category.
