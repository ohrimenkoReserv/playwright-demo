<!-- suite
id: @S3af4bff2
-->
# Key pages have no critical or serious accessibility violations

<!-- test
id: @Tf96b8f56
priority: low
tags: TC-NFR-003, ui, non-functional, REQ-NFR-03, regression
-->
## Key pages have no critical or serious accessibility violations

## Preconditions

- An axe scanner (the axe DevTools browser extension, or `@axe-core/playwright` in automation) checks the WCAG 2.0 and 2.1 level A and AA rules on the whole page.
- Product P is an ordinary in-stock product (not a rental), its ID is taken from `GET /products`.
- A new browser session: no customer is logged in.

## Steps

1. Open the home page and run the scan.
*Expected*: The scan reports no violation with impact "critical" or "serious".
2. Open the product page of P and run the scan.
*Expected*: The scan reports no violation with impact "critical" or "serious".
3. Open the login page (`/auth/login`) and run the scan.
*Expected*: The scan reports no violation with impact "critical" or "serious".
4. Open the registration page (`/auth/register`) and run the scan.
*Expected*: The scan reports no violation with impact "critical" or "serious".
5. Add P to the cart, open the cart (`/checkout`) and run the scan.
*Expected*: The scan reports no violation with impact "critical" or "serious".
6. Click "Proceed to checkout" and run the scan on the sign-in step.
*Expected*: The scan reports no violation with impact "critical" or "serious".
