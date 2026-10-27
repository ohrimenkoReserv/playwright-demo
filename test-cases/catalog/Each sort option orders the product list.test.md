<!-- suite
id: @Sdaaba76e
-->
# Each sort option orders the product list

<!-- test
id: @T73c696ec
priority: normal
tags: TC-CAT-010, ui, catalog, REQ-CAT-06, regression
-->
## Each sort option orders the product list

## Preconditions

- The catalog contains the seed data (the database is reset every hour).
- A new browser session on the home page.

## Steps

1. Select "Name (A - Z)" in the sort list.
*Expected*: The shown product names are in alphabetical order (case-insensitive).
2. Select "Name (Z - A)".
*Expected*: The shown product names are in reverse alphabetical order (case-insensitive).
3. Select "Price (High - Low)".
*Expected*: The shown regular prices (the struck-through price for discounted products) go from highest to lowest.
4. Select "Price (Low - High)".
*Expected*: The shown regular prices go from lowest to highest.
