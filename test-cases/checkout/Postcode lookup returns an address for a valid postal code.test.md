<!-- suite
-->
# Postcode lookup returns an address for a valid postal code

<!-- test
priority: low
tags: TC-CHK-009, api, checkout, REQ-CHK-07, regression
-->
## Postcode lookup returns an address for a valid postal code

## Preconditions

- No access token is needed.

## Steps

1. Send `GET /postcode-lookup` with `country` = `NL`, `postcode` = `1011AB` and `house_number` = `1`.
*Expected*: The response status is 200, `street` and `city` are not empty, and `postcode` is `1011AB`.
2. Send `GET /postcode-lookup` with `country` = `AT` and `postcode` = `1011AB`.
*Expected*: The response status is 422 and the body is `{"message": "The postal code format is not valid for the selected country."}`.
