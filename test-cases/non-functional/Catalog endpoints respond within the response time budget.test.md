<!-- suite
id: @S52454259
-->
# Catalog endpoints respond within the response time budget

<!-- test
id: @T3b3acccd
priority: low
tags: TC-NFR-002, api, non-functional, REQ-NFR-02, regression
-->
## Catalog endpoints respond within the response time budget

## Preconditions

- The budget is p95 < 1 s per endpoint (proposed, pending Q-04). The p95 of 20 calls is the 19th fastest response time.
- A product ID is taken from `GET /products`.
- Calls are sent one after another, not in parallel.

## Steps

1. Send `GET /products` 20 times and measure the response time of each call.
*Expected*: Every response has status 200 and the p95 response time is under 1 s.
2. Send `GET /products/{id}` 20 times and measure the response time of each call.
*Expected*: Every response has status 200 and the p95 response time is under 1 s.
3. Send `GET /categories/tree` 20 times and measure the response time of each call.
*Expected*: Every response has status 200 and the p95 response time is under 1 s.
