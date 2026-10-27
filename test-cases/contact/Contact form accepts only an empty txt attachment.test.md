<!-- suite
id: @S7f79bba2
-->
# Contact form accepts only an empty txt attachment

<!-- test
id: @Tb9fca34f
priority: low
tags: TC-CON-005, ui, contact, REQ-CON-03, regression
-->
## Contact form accepts only an empty txt attachment

## Preconditions

- A new browser session: no customer is logged in.
- Three local files: "empty.txt" (0 bytes), "notes.txt" (not empty) and "empty.pdf" (0 bytes).

## Steps

1. Open the contact page.
*Expected*: The attachment field shows the help text "Only files with the txt extension are allowed, and files must be 0kb."
2. Fill in first name "QA", last name "Guest", a unique email, subject "Customer service" and a message of at least 50 characters, attach "empty.pdf" and click "Send".
*Expected*: The error "File should have a txt extension." is shown and no confirmation is shown.
3. Reload the page, fill in the form again, attach "notes.txt" and click "Send".
*Expected*: The error "File should be empty." is shown and no confirmation is shown.
4. Reload the page, fill in the form again, attach "empty.txt" and click "Send".
*Expected*: The message "Thanks for your message! We will contact you shortly." is shown.
