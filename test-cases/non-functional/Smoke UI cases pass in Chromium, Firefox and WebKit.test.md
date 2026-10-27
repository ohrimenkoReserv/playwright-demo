<!-- suite
id: @S9ee68746
-->
# Smoke UI cases pass in Chromium, Firefox and WebKit

<!-- test
id: @T89ed2c68
priority: normal
tags: TC-NFR-004, ui, non-functional, REQ-NFR-04, regression
-->
## Smoke UI cases pass in Chromium, Firefox and WebKit

## Preconditions

- The UI and E2E smoke set is every case tagged `smoke` with level `ui` or `e2e`: TC-AUTH-007, TC-CART-001, TC-CAT-003, TC-CAT-012 and TC-CHK-001.
- Current stable versions of Chromium (Chrome), Firefox and WebKit (Safari) are available.

## Steps

1. Run every case of the smoke set in Chromium.
*Expected*: Every case passes.
2. Run every case of the smoke set in Firefox.
*Expected*: Every case passes.
3. Run every case of the smoke set in WebKit.
*Expected*: Every case passes.
