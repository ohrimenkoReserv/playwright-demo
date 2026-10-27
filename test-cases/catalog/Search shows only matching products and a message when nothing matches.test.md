<!-- suite
id: @S5e30a6e9
-->
# Search shows only matching products and a message when nothing matches

<!-- test
id: @T4222310d
priority: critical
tags: TC-CAT-003, ui, catalog, REQ-CAT-02, regression, smoke
-->
## Search shows only matching products and a message when nothing matches

## Preconditions

- The catalog contains the seed data (the database is reset every hour).
- A new browser session on the home page.

## Steps

1. Type "pliers" into the search field and click "Search".
*Expected*: The caption "Searched for: pliers" is shown, every shown product name contains "pliers" (case-insensitive), and the text "<n> products found for 'pliers'" shows the number of shown products.
2. Type "xyzqwerty" into the search field and click "Search".
*Expected*: The caption "Searched for: xyzqwerty", the text "0 products found for 'xyzqwerty'" and the message "There are no products found." are shown, and no product is listed.
