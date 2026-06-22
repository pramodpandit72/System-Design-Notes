# REST API Deep Dive

## Introduction

REST APIs are the most commonly used way for applications to communicate over the internet.

Whenever you:

* Login to Instagram
* Search products on Amazon
* Watch videos on YouTube
* Book a cab on Uber

Your application is likely communicating with a backend server through REST APIs.

Understanding REST APIs is essential for Full Stack Development and System Design.

---

# What is a REST API?

## Definition

REST stands for:

**Representational State Transfer**

A REST API is an architectural style that allows clients and servers to communicate using HTTP.

In simple words:

> REST API is a way for applications to exchange data over the internet using HTTP requests.

---

## Example

```text
Mobile App
      ↓
REST API
      ↓
Backend Server
      ↓
Database
```

When a user requests data, the API receives the request, processes it, and returns a response.

---

# HTTP Methods

HTTP methods define the action that should be performed on a resource.

Think of them as verbs that tell the server what to do.

The most important methods are:

* GET
* POST
* PUT
* PATCH
* DELETE

---

# GET Method

## Purpose

Used to retrieve data from the server.

## Example

Get user details.

```http
GET /users/101
```

### Response

```json
{
  "id": 101,
  "name": "Rahul",
  "email": "rahul@gmail.com"
}
```

## Characteristics

* Read-only operation
* Does not modify data
* Safe operation

---

# POST Method

## Purpose

Used to create new resources.

## Example

Create a new user.

```http
POST /users
```

### Request Body

```json
{
  "name": "Rahul",
  "email": "rahul@gmail.com"
}
```

### Response

```json
{
  "id": 101,
  "name": "Rahul",
  "email": "rahul@gmail.com"
}
```

## Characteristics

* Creates new data
* Changes server state

---

# PUT Method

## Purpose

Used to completely replace an existing resource.

## Example

Update user information.

```http
PUT /users/101
```

### Request Body

```json
{
  "name": "Rahul Sharma",
  "email": "rahul@gmail.com"
}
```

The entire resource gets replaced.

---

## Visual Example

Before:

```json
{
  "name": "Rahul",
  "email": "rahul@gmail.com"
}
```

After PUT:

```json
{
  "name": "Rahul Sharma",
  "email": "rahul@gmail.com"
}
```

---

# PATCH Method

## Purpose

Used to partially update a resource.

Only specific fields are modified.

## Example

```http
PATCH /users/101
```

### Request Body

```json
{
  "name": "Rahul Sharma"
}
```

Only the name changes.

The remaining fields stay unchanged.

---

## PUT vs PATCH

### PUT

Replaces entire resource.

```json
{
  "name": "Rahul Sharma",
  "email": "rahul@gmail.com"
}
```

### PATCH

Updates only specified fields.

```json
{
  "name": "Rahul Sharma"
}
```

---

# DELETE Method

## Purpose

Used to remove a resource.

## Example

```http
DELETE /users/101
```

The user with ID 101 is deleted.

---

# HTTP Methods Summary

| Method | Purpose                 |
| ------ | ----------------------- |
| GET    | Read Data               |
| POST   | Create Data             |
| PUT    | Replace Entire Resource |
| PATCH  | Partial Update          |
| DELETE | Remove Resource         |

---

# Endpoints

## Definition

An endpoint is a URL where an API can be accessed.

In simple words:

> Endpoint is the address of a specific API resource.

---

## Example

```text
https://api.company.com/users
```

Here:

```text
/users
```

is the endpoint.

---

## Multiple Endpoints Example

```http
GET /users
GET /users/101
POST /users
DELETE /users/101
GET /orders
GET /products
```

Each endpoint represents a resource.

---

# JSON

## Definition

JSON stands for:

**JavaScript Object Notation**

It is the most commonly used data format in REST APIs.

---

## Example

```json
{
  "id": 101,
  "name": "Rahul",
  "email": "rahul@gmail.com"
}
```

---

## Why JSON Is Popular

* Lightweight
* Human-readable
* Easy to parse
* Language-independent

---

# Query Parameters

## Definition

Query parameters are used to send optional information to an API.

They are added after a question mark (?).

---

## Example

```http
GET /products?page=1
```

Here:

```text
page=1
```

is a query parameter.

---

## Multiple Query Parameters

```http
GET /products?page=1&limit=10
```

### Meaning

```text
page = 1
limit = 10
```

Return first page with 10 products.

---

## Search Example

```http
GET /products?category=laptop
```

Return only laptop products.

---

# Request Body

## Definition

Request Body contains data sent from client to server.

Usually used with:

* POST
* PUT
* PATCH

---

## Example

```http
POST /users
```

### Request Body

```json
{
  "name": "Rahul",
  "email": "rahul@gmail.com"
}
```

The server uses this data to create a new user.

---

# Response Body

## Definition

Response Body contains data returned by the server.

---

## Example

```json
{
  "id": 101,
  "name": "Rahul",
  "email": "rahul@gmail.com"
}
```

The server sends this data back to the client.

---

# Request and Response Flow

```text
Client
   ↓
Request
(Method + URL + Body)
   ↓
Server
   ↓
Response
(Status Code + Data)
   ↓
Client
```

---

# Status Codes

## Definition

Status codes indicate the result of an API request.

They help clients understand whether the request succeeded or failed.

---

# 2xx Success Codes

### 200 OK

Request successful.

```http
200 OK
```

---

### 201 Created

Resource successfully created.

```http
201 Created
```

Usually returned after POST requests.

---

# 3xx Redirection Codes

### 301 Moved Permanently

Resource moved permanently.

```http
301 Moved Permanently
```

---

# 4xx Client Error Codes

### 400 Bad Request

Invalid request.

```http
400 Bad Request
```

---

### 401 Unauthorized

Authentication required.

```http
401 Unauthorized
```

---

### 403 Forbidden

Access denied.

```http
403 Forbidden
```

---

### 404 Not Found

Resource does not exist.

```http
404 Not Found
```

---

# 5xx Server Error Codes

### 500 Internal Server Error

Unexpected server failure.

```http
500 Internal Server Error
```

---

### 503 Service Unavailable

Server temporarily unavailable.

```http
503 Service Unavailable
```

---

# Common Status Codes Summary

| Code | Meaning               |
| ---- | --------------------- |
| 200  | Success               |
| 201  | Resource Created      |
| 400  | Bad Request           |
| 401  | Unauthorized          |
| 403  | Forbidden             |
| 404  | Not Found             |
| 500  | Internal Server Error |
| 503  | Service Unavailable   |

---

# API Design Best Practices

Good API design makes systems easier to understand, maintain, and scale.

---

## 1. Use Nouns Instead of Verbs

### Bad

```http
GET /getUsers
POST /createUser
```

### Good

```http
GET /users
POST /users
```

Resources should be nouns.

---

## 2. Use Proper HTTP Methods

### Correct

```http
GET /users
POST /users
PUT /users/101
DELETE /users/101
```

Do not use GET for creating data.

---

## 3. Use Meaningful Resource Names

### Bad

```http
GET /data
```

### Good

```http
GET /users
GET /products
GET /orders
```

Endpoints should clearly describe resources.

---

## 4. Use Consistent Naming

### Good

```http
/users
/products
/orders
```

Avoid mixing styles.

### Bad

```http
/users
/getProducts
/order_data
```

---

## 5. Version Your APIs

### Example

```http
/api/v1/users
/api/v2/users
```

Versioning prevents breaking existing clients.

---

## 6. Return Proper Status Codes

### Good

```http
200 OK
201 Created
404 Not Found
500 Internal Server Error
```

Avoid always returning 200.

---

## 7. Support Pagination

For large datasets:

```http
GET /products?page=1&limit=20
```

Benefits:

* Faster responses
* Reduced memory usage
* Better scalability

---

## 8. Use HTTPS

Always secure APIs.

### Good

```text
https://api.company.com/users
```

### Bad

```text
http://api.company.com/users
```

HTTPS encrypts data during transmission.

---

## 9. Use Clear Error Messages

### Bad

```json
{
  "error": "Something went wrong"
}
```

### Good

```json
{
  "error": "User with ID 101 not found"
}
```

Clear errors simplify debugging.

---

## 10. Keep APIs Stateless

Each request should contain all necessary information.

The server should not depend on previous requests.

This is one of the core REST principles.

---

# Example REST API Design

## User Resource

### Get All Users

```http
GET /users
```

### Get User By ID

```http
GET /users/101
```

### Create User

```http
POST /users
```

### Update User

```http
PUT /users/101
```

### Partially Update User

```http
PATCH /users/101
```

### Delete User

```http
DELETE /users/101
```

This follows REST conventions perfectly.

---

# Key Takeaways

## HTTP Methods

* GET → Read Data
* POST → Create Data
* PUT → Replace Resource
* PATCH → Partial Update
* DELETE → Remove Resource

## Endpoints

* API addresses where resources are accessed.
* Example: `/users`, `/orders`, `/products`

## JSON

* Standard format for API communication.
* Lightweight and human-readable.

## Query Parameters

Used for:

* Filtering
* Searching
* Pagination
* Sorting

Example:

```http
GET /products?page=1&limit=10
```

## Status Codes

Tell clients whether a request succeeded or failed.

Most common:

* 200
* 201
* 400
* 401
* 403
* 404
* 500

## API Design Best Practices

* Use nouns for resources.
* Follow HTTP standards.
* Version APIs.
* Return proper status codes.
* Use pagination.
* Keep APIs stateless.
* Always use HTTPS.

## Final Note

A well-designed REST API is simple, predictable, scalable, and easy to maintain. Good API design improves developer experience, system reliability, and long-term scalability.
