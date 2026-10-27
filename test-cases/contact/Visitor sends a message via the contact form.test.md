<!-- suite
id: @S1838aeef
-->
# Visitor sends a message via the contact form

<!-- test
id: @Te4180584
priority: normal
tags: TC-CON-001, ui, contact, REQ-CON-01, regression
-->
## Visitor sends a message via the contact form

## Preconditions

- A new browser session: no customer is logged in.

## Steps

1. Open the contact page (`/contact`).
*Expected*: The page "Contact" shows the fields first name, last name, email, subject, message and attachment, and the "Send" button.
2. Fill in first name "QA", last name "Guest", a unique email, subject "Customer service" and a message of at least 50 characters, and click "Send".
*Expected*: The message "Thanks for your message! We will contact you shortly." is shown instead of the form.
