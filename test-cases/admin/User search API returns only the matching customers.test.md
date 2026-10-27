<!-- suite
id: @Sf1cd2306
-->
# User search API returns only the matching customers

<!-- test
id: @Tc02e88ad
priority: low
tags: TC-ADM-008, api, admin, REQ-ADM-06, regression
-->
## User search API returns only the matching customers

## Preconditions

- The seed admin account is logged in via `POST /users/login` and has an access token (credentials come from the team secrets and are never written in the case).
- S is a unique suffix of digits for this run (e.g. a timestamp).
- Customer A is registered via `POST /users/register` with the last name "QasearchS" (one word) and a unique email; customer B with another last name and a unique email.

## Steps

1. Send `GET /users/search?q={email of A}` with the admin token.
*Expected*: The response status is 200 and `data` has exactly one user: A.
2. Send `GET /users/search?q=QasearchS` with the admin token.
*Expected*: The response status is 200, `data` contains A, B is not listed, and every user in `data` has "QasearchS" in the first name, last name, email or city.
3. Send `GET /users/search?q=zzqxnomatch` with the admin token.
*Expected*: The response status is 200, `total` = 0 and `data` is empty.
