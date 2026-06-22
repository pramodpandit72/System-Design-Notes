# APIs and Communication

## Introduction

Modern applications are made up of multiple components that need to communicate with each other.

For example:

* Mobile App ↔ Backend Server
* Frontend ↔ Backend
* Backend ↔ Database
* Microservice ↔ Microservice
* Payment Service ↔ E-Commerce Application

This communication is usually done through **APIs (Application Programming Interfaces)**.

Understanding APIs is one of the most important concepts in System Design.

---

# What is an API?

## Definition

API stands for **Application Programming Interface**.

An API is a set of rules that allows two software applications to communicate with each other.

In simple words:

> An API is a messenger that takes a request from one system and returns a response from another system.

---

## Real-Life Example

Imagine you are in a restaurant.

```text
Customer
    ↓
Waiter
    ↓
Kitchen
    ↓
Waiter
    ↓
Customer
```

Here:

* Customer = Client
* Kitchen = Server
* Waiter = API

The waiter takes your request to the kitchen and brings back the result.

Similarly, APIs help applications communicate.

---

## Example

When you log in to Instagram:

```text
Mobile App
      ↓
Login API
      ↓
Backend Server
      ↓
Response
```

The API sends your username and password to the server and returns the result.

---

# REST APIs

## Definition

REST stands for:

**Representational State Transfer**

REST is the most commonly used API architecture for web applications.

REST APIs communicate using HTTP.

---

## Characteristics

* Stateless
* Uses HTTP
* Simple to understand
* Widely adopted
* Resource-based

---

## Common HTTP Methods

### GET

Retrieve data.

```http
GET /users/101
```

Example:

Get user information.

---

### POST

Create new data.

```http
POST /users
```

Example:

Create a new user account.

---

### PUT

Update existing data.

```http
PUT /users/101
```

---

### DELETE

Delete data.

```http
DELETE /users/101
```

---

## REST Response Example

```json
{
  "id": 101,
  "name": "Rahul",
  "email": "rahul@gmail.com"
}
```

Usually, REST APIs use JSON.

---

## Advantages

* Easy to learn
* Human-readable
* Language-independent
* Excellent browser support
* Large ecosystem

---

## Disadvantages

* Over-fetching data
* Under-fetching data
* Multiple API calls may be required

---

## Common Use Cases

* Web Applications
* Mobile Applications
* Public APIs
* E-Commerce Systems

---

# SOAP APIs

## Definition

SOAP stands for:

**Simple Object Access Protocol**

SOAP is a protocol used for communication between systems.

Unlike REST, SOAP follows strict standards.

---

## Characteristics

* XML-based
* Highly standardized
* Strong security support
* Built-in error handling

---

## SOAP Request Example

```xml
<soap:Envelope>
   <soap:Body>
      <GetUser>
         <UserId>101</UserId>
      </GetUser>
   </soap:Body>
</soap:Envelope>
```

---

## Advantages

* High security
* Standardized protocol
* Reliable transactions
* Enterprise-friendly

---

## Disadvantages

* Complex
* Verbose XML format
* Slower than REST
* Larger payload size

---

## Common Use Cases

* Banking Systems
* Payment Systems
* Enterprise Software
* Government Applications

---

# GraphQL

## Definition

GraphQL is a query language for APIs developed by Facebook.

It allows clients to request exactly the data they need.

---

## Problem with REST

Suppose a frontend needs:

* User Name
* User Email

REST may return:

```json
{
  "id": 101,
  "name": "Rahul",
  "email": "rahul@gmail.com",
  "address": "...",
  "phone": "...",
  "country": "..."
}
```

Extra data is returned.

This is called:

```text
Over-Fetching
```

---

## GraphQL Solution

Client requests only required fields.

### Query

```graphql
{
  user(id: 101) {
    name
    email
  }
}
```

### Response

```json
{
  "data": {
    "user": {
      "name": "Rahul",
      "email": "rahul@gmail.com"
    }
  }
}
```

Only requested data is returned.

---

## Advantages

* No over-fetching
* No under-fetching
* Single endpoint
* Flexible queries

---

## Disadvantages

* More complex implementation
* Difficult caching
* Higher server complexity

---

## Common Use Cases

* Social Media Applications
* Mobile Applications
* Complex Frontends
* Data-heavy Applications

---

# gRPC

## Definition

gRPC is a high-performance communication framework developed by Google.

It uses:

```text
Protocol Buffers (Protobuf)
```

instead of JSON.

---

## How gRPC Works

```text
Client
    ↓
gRPC Request
    ↓
Server
    ↓
gRPC Response
```

Data is sent in binary format.

---

## Example

Instead of JSON:

```json
{
  "id": 101,
  "name": "Rahul"
}
```

gRPC converts data into compact binary format.

This reduces:

* Network usage
* Response size
* Processing time

---

## Advantages

* Extremely fast
* Small payloads
* Strong typing
* Efficient communication

---

## Disadvantages

* Harder to debug
* Browser limitations
* Less human-readable

---

## Common Use Cases

* Microservices Communication
* Internal Backend Services
* High-Performance Systems
* Real-Time Systems

---

# WebSockets

## Definition

WebSocket is a communication protocol that enables real-time, two-way communication between client and server.

Unlike REST, the connection remains open.

---

## REST Communication

For every request:

```text
Client
    ↓
Request
    ↓
Server
    ↓
Response
```

Connection closes.

---

## WebSocket Communication

```text
Client
      ↕
Persistent Connection
      ↕
Server
```

Connection remains open.

Both sides can send messages anytime.

---

## Example

WhatsApp Chat

When a friend sends a message:

```text
Friend Sends Message
        ↓
Server
        ↓
Instantly Delivered
```

No need for continuous requests.

---

## Advantages

* Real-time communication
* Low latency
* Efficient for frequent updates
* Full duplex communication

---

## Disadvantages

* More complex infrastructure
* Persistent connections consume resources
* Scaling is harder

---

## Common Use Cases

* Chat Applications
* Live Notifications
* Online Gaming
* Stock Market Updates
* Collaborative Tools

---

# When and Why to Use Each One

## Use REST APIs When

* Building standard web applications
* Creating public APIs
* Simplicity is important
* JSON responses are sufficient

### Examples

* E-Commerce APIs
* Blog APIs
* User Management Systems

---

## Use SOAP APIs When

* Security is critical
* Enterprise standards are required
* Transactions must be highly reliable

### Examples

* Banking Systems
* Insurance Systems
* Government Platforms

---

## Use GraphQL When

* Frontend needs flexible data
* Multiple resources are fetched together
* Mobile apps need optimized responses

### Examples

* Facebook
* Instagram
* Complex Dashboards

---

## Use gRPC When

* Speed is critical
* Internal service communication is needed
* Large-scale microservices architecture exists

### Examples

* Google Internal Services
* High-Performance Backend Systems

---

## Use WebSockets When

* Real-time updates are required
* Server needs to push data instantly
* Continuous communication is needed

### Examples

* WhatsApp
* Discord
* Multiplayer Games
* Live Trading Platforms

---

# Comparison Table

| Feature             | REST             | SOAP               | GraphQL                | gRPC          | WebSocket       |
| ------------------- | ---------------- | ------------------ | ---------------------- | ------------- | --------------- |
| Communication Style | Request-Response | Request-Response   | Query-Based            | RPC           | Full Duplex     |
| Data Format         | JSON             | XML                | JSON                   | Protobuf      | Custom Messages |
| Performance         | Good             | Moderate           | Good                   | Very Fast     | Very Fast       |
| Human Readable      | Yes              | Yes                | Yes                    | No            | Depends         |
| Real-Time Support   | No               | No                 | Limited                | Limited       | Yes             |
| Complexity          | Low              | High               | Medium                 | Medium        | Medium          |
| Best For            | Public APIs      | Enterprise Systems | Flexible Data Fetching | Microservices | Real-Time Apps  |

---

# Interview Perspective

A common System Design interview question is:

> Which communication protocol would you choose and why?

### Typical Answers

#### Frontend ↔ Backend

Use REST or GraphQL.

#### Microservice ↔ Microservice

Use gRPC.

#### Chat Application

Use WebSockets.

#### Banking System

Use SOAP.

The answer depends on system requirements.

---

# Key Takeaways

## REST

* Most popular API style.
* Uses HTTP and JSON.
* Easy to build and maintain.

## SOAP

* XML-based protocol.
* Secure and reliable.
* Common in enterprise systems.

## GraphQL

* Client requests exactly the required data.
* Solves over-fetching and under-fetching problems.

## gRPC

* High-performance communication framework.
* Uses Protocol Buffers.
* Excellent for microservices.

## WebSockets

* Persistent connection.
* Enables real-time communication.
* Ideal for chat and live updates.

## Final Note

There is no single best communication method.

The choice depends on:

* Performance requirements
* Scalability needs
* Security requirements
* Real-time communication needs
* System complexity

A good System Designer chooses the communication mechanism that best fits the application's requirements.
