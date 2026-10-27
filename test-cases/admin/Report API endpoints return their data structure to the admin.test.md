<!-- suite
id: @S62ec9d25
-->
# Report API endpoints return their data structure to the admin

<!-- test
id: @T30f018fb
priority: low
tags: TC-ADM-009, api, admin, REQ-ADM-07, regression
-->
## Report API endpoints return their data structure to the admin

## Preconditions

- The seed admin account is logged in via `POST /users/login` and has an access token (credentials come from the team secrets and are never written in the case).
- The report endpoints allow 60 requests per minute.

## Steps

1. Send `GET /reports/total-sales-of-years` with the admin token.
*Expected*: The response status is 200 and the body is a list with one item for last year and one for this year, each with `year` and `total`.
2. Send `GET /reports/total-sales-per-country` with the admin token.
*Expected*: The response status is 200 and every item has `total_sales` and `billing_country`.
3. Send `GET /reports/top10-purchased-products` with the admin token.
*Expected*: The response status is 200, the list has at most 10 items, and every item has `name` and `count`.
4. Send `GET /reports/top10-best-selling-categories` with the admin token.
*Expected*: The response status is 200, the list has at most 10 items, and every item has `category_name` and `total_earned`.
5. Send `GET /reports/customers-by-country` with the admin token.
*Expected*: The response status is 200 and every item has `amount` and `country`.
6. Send `GET /reports/average-sales-per-month` with the admin token.
*Expected*: The response status is 200 and the list has 12 items with `month` 1 to 12, each with `average` and `amount`.
7. Send `GET /reports/average-sales-per-week` with the admin token.
*Expected*: The response status is 200 and the list has 52 items with `week` 1 to 52, each with `average` and `amount`.
