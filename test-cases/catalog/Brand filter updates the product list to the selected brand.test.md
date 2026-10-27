<!-- suite
id: @Sa6017187
-->
# Brand filter updates the product list to the selected brand

<!-- test
id: @Td8991959
priority: normal
tags: TC-CAT-008, ui, catalog, REQ-CAT-04, regression
-->
## Brand filter updates the product list to the selected brand

## Preconditions

- The catalog contains the seed data (the database is reset every hour).
- The names of the products of the brands "ForgeFlex Tools" and "MightyCraft Hardware" are taken from `GET /products?by_brand={brand ID}` (all pages).
- A new browser session on the home page.

## Steps

1. In the filters, tick the brand "ForgeFlex Tools".
*Expected*: The product list updates and every shown product is one of the "ForgeFlex Tools" products.
2. Untick "ForgeFlex Tools" and tick "MightyCraft Hardware".
*Expected*: The product list updates and every shown product is one of the "MightyCraft Hardware" products.
