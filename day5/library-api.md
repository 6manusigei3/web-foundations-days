# Library Books REST API

## Introduction

The Library Books REST API allows users to retrieve, create, update, and delete books. It follows REST principles and uses HTTP methods and status codes to communicate with the server.

Each book contains an ID, title, author, and publication year.

## 1. List All Books

* **Method:** GET
* **Path:** `/books`
* **Description:** Retrieves all books in the library.
* **Success status:** `200 OK`

Example request:

```http
GET /books
```

Example response:

```json
[
  {
    "id": 1,
    "title": "The Great Gatsby",
    "author": "F. Scott Fitzgerald",
    "year": 1925
  },
  {
    "id": 2,
    "title": "Things Fall Apart",
    "author": "Chinua Achebe",
    "year": 1958
  }
]
```

## 2. Get a Single Book

* **Method:** GET
* **Path:** `/books/{id}`
* **Description:** Retrieves a book using its unique ID.
* **Success status:** `200 OK`

Example request:

```http
GET /books/1
```

Example response:

```json
{
  "id": 1,
  "title": "The Great Gatsby",
  "author": "F. Scott Fitzgerald",
  "year": 1925
}
```

If the book does not exist, the server returns `404 Not Found`.

## 3. Create a Book

* **Method:** POST
* **Path:** `/books`
* **Description:** Creates a new book in the library.
* **Success status:** `201 Created`

Example request:

```http
POST /books
Content-Type: application/json
```

Example JSON request body:

```json
{
  "title": "The River and the Source",
  "author": "Margaret Ogola",
  "year": 1994
}
```

Example response:

```json
{
  "id": 3,
  "title": "The River and the Source",
  "author": "Margaret Ogola",
  "year": 1994
}
```

The server generates the ID for the new book.

## 4. Update a Book

* **Method:** PUT
* **Path:** `/books/{id}`
* **Description:** Replaces the details of an existing book.
* **Success status:** `200 OK`

Example request:

```http
PUT /books/1
Content-Type: application/json
```

Example JSON request body:

```json
{
  "title": "The Great Gatsby - Revised Edition",
  "author": "F. Scott Fitzgerald",
  "year": 1925
}
```

Example response:

```json
{
  "id": 1,
  "title": "The Great Gatsby - Revised Edition",
  "author": "F. Scott Fitzgerald",
  "year": 1925
}
```

If the book does not exist, the server returns `404 Not Found`.

## 5. Delete a Book

* **Method:** DELETE
* **Path:** `/books/{id}`
* **Description:** Deletes a book using its unique ID.
* **Success status:** `204 No Content`

Example request:

```http
DELETE /books/1
```

A successful deletion returns no response body.

If the book does not exist, the server returns `404 Not Found`.

## 6. Filter Books by Author

* **Method:** GET
* **Path:** `/books?author={author}`
* **Description:** Retrieves books written by the specified author using a query parameter.
* **Success status:** `200 OK`

Example request:

```http
GET /books?author=Chinua%20Achebe
```

Example response:

```json
[
  {
    "id": 2,
    "title": "Things Fall Apart",
    "author": "Chinua Achebe",
    "year": 1958
  }
]
```

The author parameter should be URL-encoded when necessary. If no books match, the API returns `200 OK` with an empty array.

## Error Responses

### 400 Bad Request

**Meaning:** The server cannot process the request because the submitted data is invalid or required fields are missing.

Example request:

```http
POST /books
Content-Type: application/json
```

Example invalid JSON request body:

```json
{
  "title": "",
  "author": "",
  "year": "not-a-year"
}
```

Example error response:

```json
{
  "error": "Bad Request",
  "message": "Title, author, and a valid publication year are required."
}
```

The server returns `400 Bad Request` when the request body fails validation.

### 404 Not Found

**Meaning:** The requested book does not exist.

Example request:

```http
GET /books/9999
```

Example error response:

```json
{
  "error": "Not Found",
  "message": "Book with ID 9999 was not found."
}
```

The server returns `404 Not Found` when a requested book ID does not exist.

## Summary

This API defines six endpoints for listing, retrieving, creating, updating, deleting, and filtering books. It uses appropriate HTTP methods, success status codes, JSON payloads, and error responses to provide a clear RESTful API contract.
