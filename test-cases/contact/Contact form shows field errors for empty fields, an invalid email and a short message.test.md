<!-- suite
id: @Sa0509c01
-->
# Contact form shows field errors for empty fields, an invalid email and a short message

<!-- test
id: @T2d8839a8
priority: normal
tags: TC-CON-003, ui, contact, REQ-CON-02, regression
-->
## Contact form shows field errors for empty fields, an invalid email and a short message

## Preconditions

- A new browser session: no customer is logged in.

## Steps

1. Open the contact page and click "Send" without filling in any field.
*Expected*: The errors "First name is required", "Last name is required", "Email is required", "Subject is required" and "Message is required" are shown, and no confirmation is shown.
2. Fill in first name "QA", last name "Guest", a unique email, subject "Customer service" and a message of at least 50 characters, change the email to "qa-invalid-email" and click "Send".
*Expected*: The error "Email format is invalid" is shown and no confirmation is shown.
3. Change the email to a valid one, change the message to "Too short", click outside the message field and click "Send".
*Expected*: The error "Message must be minimal 50 characters" is shown and no confirmation is shown.
