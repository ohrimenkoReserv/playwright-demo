<!-- suite
id: @S6789a509
-->
# Login API returns an access token for valid credentials

<!-- test
id: @Te963a5ed
priority: critical
tags: TC-AUTH-008, api, auth, REQ-AUTH-05, regression, smoke
-->
## Login API returns an access token for valid credentials

## Preconditions

- A new customer account is registered via the API (`POST /users/register`) with a unique
  email and a valid password.

## Steps

1. Send `POST /users/login` with the customer's email and password in the JSON body.
*Expected*: The response status is 200. The body has `access_token` (a JWT: a non-empty string of three dot-separated parts), `token_type` equal to `bearer` (case-insensitive) and a positive number `expires_in`.
