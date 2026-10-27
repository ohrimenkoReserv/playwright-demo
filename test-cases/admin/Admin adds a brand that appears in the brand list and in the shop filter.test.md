<!-- suite
id: @Sbff96e12
-->
# Admin adds a brand that appears in the brand list and in the shop filter

<!-- test
id: @Tec1f8af0
priority: normal
tags: TC-ADM-002, ui, admin, REQ-ADM-01, regression
-->
## Admin adds a brand that appears in the brand list and in the shop filter

## Preconditions

- The seed admin account is logged in via the login form (credentials come from the team secrets and are never written in the case).
- S is a unique suffix for this run (e.g. a timestamp), so names and slugs do not clash with other data.

## Steps

1. Open the admin brands page (`/admin/brands`) and click "Add Brand".
*Expected*: The page "Add Brand" with the fields "Name" and "Slug" is shown.
2. Enter the name "QA Brand S" and the slug "qa-brand-s" and click "Save".
*Expected*: The message "Brand saved!" is shown.
3. Open the admin brands page again.
*Expected*: The list has a row with the name "QA Brand S" and the slug "qa-brand-s".
4. Open the shop home page.
*Expected*: The brand filter in the sidebar lists "QA Brand S".
