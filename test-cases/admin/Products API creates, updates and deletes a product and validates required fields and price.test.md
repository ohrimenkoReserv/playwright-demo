<!-- suite
id: @S3a1fc74e
-->
# Products API creates, updates and deletes a product and validates required fields and price

<!-- test
id: @Td238a461
priority: normal
tags: TC-ADM-004, api, admin, REQ-ADM-03, regression
-->
## Products API creates, updates and deletes a product and validates required fields and price

## Preconditions

- The seed admin account is logged in via `POST /users/login` and has an access token (credentials come from the team secrets and are never written in the case).
- S is a unique suffix for this run (e.g. a timestamp), so names and slugs do not clash with other data.
- A brand ID, a category ID and a product image ID are taken from `GET /brands`, `GET /categories` and `GET /images`.

## Steps

1. Send `POST /products` with `name` = "QAProductS", a description, `price` = 19.99, the brand, category and image IDs, `is_location_offer` = false, `is_rental` = false and the admin token.
*Expected*: The response status is 201 and the body has the product `id`, `name` = "QAProductS" and `price` = 19.99.
2. Send `GET /products/{id}`.
*Expected*: The response status is 200, and `name`, `price`, `brand.id` and `category.id` equal the values sent.
3. Send `PUT /products/{id}` with the same data, `price` = 24.5 and the admin token.
*Expected*: The response status is 200, the body is `{"success": true}`, and `GET /products/{id}` returns `price` = 24.5.
4. Send `POST /products` with an empty body.
*Expected*: The response status is 422 with "The … field is required." errors for `name`, `price`, `category_id`, `brand_id`, `is_location_offer`, `is_rental` and `product_image_id`.
5. Send `POST /products` with the data from step 1 but `price` = "abc".
*Expected*: The response status is 422 with a `price` error "The price field must be a number."
6. Send `DELETE /products/{id}` with the admin token.
*Expected*: The response status is 204, and `GET /products/{id}` returns 404 with `{"message": "Requested item not found"}`.
