<!-- suite
id: @S8d4a8ec9
-->
# Customer updates the profile and sees the changes after reload

<!-- test
id: @T073ce4d5
priority: normal
tags: TC-ACC-001, ui, account, REQ-ACC-01, regression
-->
## Customer updates the profile and sees the changes after reload

## Preconditions

- A new customer account is registered via the API (`POST /users/register`) with a unique email and a unique valid password (the API rejects passwords found in data leaks).
- The customer is logged in via the login form.

## Steps

1. Open the profile page (`/account/profile`).
*Expected*: The form shows the customer's current data.
2. Change the phone and the street to new values and click "Update Profile".
*Expected*: The message "Your profile is successfully updated!" is shown.
3. Reload the page.
*Expected*: The phone and street fields show the new values.
