<!-- suite
id: @Sd915c051
-->
# Register API rejects a postal code that does not match the country

<!-- test
id: @Tebe541fb
priority: low
tags: TC-AUTH-006, api, auth, REQ-AUTH-04, regression
-->
## Register API rejects a postal code that does not match the country

## Preconditions

- Each request uses a new unique email and otherwise valid registration data.

## Steps

1. Send `POST /users/register` with `address.country` = `DE` and `address.postal_code` = `1234`.
*Expected*: The response status is 422 and `address.postal_code` contains "The postal code format is not valid for the selected country."
2. Send `POST /users/register` with `address.country` = `DE` and `address.postal_code` = `10115`.
*Expected*: The response status is 201.
