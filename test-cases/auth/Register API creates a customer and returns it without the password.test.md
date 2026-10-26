<!-- suite
id: @Sc080e780
-->
# Register API creates a customer and returns it without the password

<!-- test
id: @T89a07416
priority: critical
tags: TC-AUTH-002, api, auth, REQ-AUTH-01, regression
-->
## Register API creates a customer and returns it without the password

## Preconditions

- Test data: a unique email and a unique valid password.

## Steps

1. Send `POST /users/register` with a valid body: `first_name`, `last_name`, `address` (`street`, `city`, `state`, `country`, `postal_code`), `phone`, `dob`, `email`, `password`.
*Expected*: The response status is 201. The body matches the `UserResponse` schema, its `id` is set, `email`, `first_name` and `last_name` equal the request, and the body has no `password` field.
2. Send `POST /users/login` with the same email and password.
*Expected*: The response status is 200 and the body has an `access_token`.
