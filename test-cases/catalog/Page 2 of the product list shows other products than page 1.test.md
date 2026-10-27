<!-- suite
id: @S0ffd96d4
-->
# Page 2 of the product list shows other products than page 1

<!-- test
id: @T2a7db480
priority: normal
tags: TC-CAT-002, ui, catalog, REQ-CAT-01, regression
-->
## Page 2 of the product list shows other products than page 1

## Preconditions

- The catalog contains the seed data (the database is reset every hour).
- A new browser session on the home page product list, with no filter, search or sorting applied.

## Steps

1. Open the home page and note the names of the shown products.
*Expected*: The product list shows 9 products, and the pagination below it has page 1 active.
2. Click page "2" in the pagination.
*Expected*: The list shows up to 9 products, none of them was shown on page 1, page 2 is active and page 1 is no longer active.
