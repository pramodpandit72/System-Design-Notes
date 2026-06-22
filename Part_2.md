# Functional vs Non-Functional Requirements

## Introduction

Before designing any software system, we must understand **what the system should do** and **how well the system should perform**.

These requirements are divided into two categories:

1. Functional Requirements
2. Non-Functional Requirements

Understanding both is essential because a system may have all the required features but still fail if it is slow, unreliable, or insecure.

---

# Functional Requirements

## Definition

Functional Requirements describe **what a system should do**.

They define the features, functions, and business logic of the application.

In simple words:

> Functional Requirements tell us what services the system must provide to users.

## Examples

For an E-Commerce Application:

* User can register an account.
* User can log in.
* User can search products.
* User can add products to cart.
* User can place an order.
* User can make payments.

These features directly represent the functionality of the system.

## Characteristics

* Feature-focused
* Describe user actions
* Define business logic
* Usually written as use cases

## Example: Instagram

Functional Requirements:

* Users can upload photos.
* Users can upload videos.
* Users can like posts.
* Users can comment on posts.
* Users can follow other users.
* Users can send messages.

---

# Non-Functional Requirements

## Definition

Non-Functional Requirements describe **how the system should perform while providing its functionality**.

They focus on system quality attributes.

In simple words:

> Non-Functional Requirements define the quality and behavior of a system.

## Examples

* System should handle 1 million users.
* Response time should be less than 200 ms.
* System should be available 99.99% of the time.
* User data should be encrypted.

These requirements do not add new features but improve the quality of the system.

---

# Scalability

## Definition

Scalability is the ability of a system to handle increasing traffic, users, or data without performance degradation.

## Why It Is Important

As users grow, the system must continue working efficiently.

A system that works for 1,000 users may fail for 1 million users if it is not scalable.

## Example

Suppose an online shopping website receives:

* 1,000 requests/day initially
* 1,000,000 requests/day after becoming popular

The system should be able to handle the increased load.

## Types of Scalability

### Vertical Scaling

Increase resources of a single server.

Example:

```text
4 GB RAM → 16 GB RAM
2 CPU → 16 CPU
```

### Horizontal Scaling

Add more servers.

Example:

```text
Server 1
Server 2
Server 3
Server 4
```

Most modern systems prefer horizontal scaling.

---

# Availability

## Definition

Availability is the percentage of time a system remains operational and accessible to users.

## Formula

```text
Availability = Uptime / Total Time
```

## Example

If a service runs throughout the year with very little downtime:

```text
Availability = 99.99%
```

## Why It Is Important

Users expect services to be available all the time.

Examples:

* Banking Systems
* Amazon
* Netflix
* Instagram

Downtime can result in loss of revenue and user trust.

---

# Reliability

## Definition

Reliability is the ability of a system to consistently perform its intended functions correctly.

## Why It Is Important

Users expect accurate and consistent results.

A reliable system:

* Does not lose data
* Produces correct results
* Recovers from failures

## Example

When money is transferred between bank accounts:

```text
Account A → ₹1000 deducted
Account B → ₹1000 added
```

The transaction must happen correctly every time.

Reliability is critical in financial systems.

---

# Performance

## Definition

Performance measures how fast and efficiently a system responds to user requests.

## Common Metrics

### Response Time

Time taken to respond to a request.

Example:

```text
Search Request → 150 ms
```

### Throughput

Number of requests processed per second.

Example:

```text
10,000 requests/second
```

### Latency

Delay between sending a request and receiving a response.

## Why It Is Important

Users prefer fast applications.

Even a small delay can reduce user satisfaction.

Examples:

* Google Search
* Instagram Feed Loading
* Amazon Product Search

---

# Security

## Definition

Security protects systems, applications, and data from unauthorized access and attacks.

## Objectives of Security

### Confidentiality

Only authorized users can access data.

### Integrity

Data cannot be modified without permission.

### Availability

Authorized users can access services when needed.

## Common Security Mechanisms

* Authentication
* Authorization
* Encryption
* Firewalls
* Rate Limiting
* Multi-Factor Authentication (MFA)

## Example

When you log in to a website:

```text
Username + Password
        ↓
Authentication
        ↓
Access Granted
```

Security ensures attackers cannot access user accounts.

---

# Maintainability

## Definition

Maintainability is the ease with which a system can be modified, fixed, updated, or improved.

## Why It Is Important

Software continuously evolves.

Developers need to:

* Fix bugs
* Add features
* Improve performance
* Upgrade technologies

A maintainable system reduces development effort and cost.

## Characteristics

* Clean code
* Modular design
* Proper documentation
* Reusable components
* Consistent coding standards

## Example

Microservices are often easier to maintain than large monolithic systems because components are separated.

---

# Observability

## Definition

Observability is the ability to understand the internal state of a system by analyzing its outputs.

In simple words:

> Observability helps engineers understand what is happening inside a system without directly looking at the code.

## Why It Is Important

When issues occur in production, developers need to quickly identify:

* What failed
* Why it failed
* Where it failed

## Three Pillars of Observability

### Logs

Record system events.

Example:

```text
User Login Successful
Payment Failed
Database Connection Error
```

### Metrics

Numerical measurements of system health.

Example:

```text
CPU Usage
Memory Usage
Response Time
Error Rate
```

### Traces

Track a request across multiple services.

Example:

```text
User Request
    ↓
API Service
    ↓
Payment Service
    ↓
Database
```

Developers can see where delays or failures occurred.

---

# Functional vs Non-Functional Requirements Comparison

| Feature         | Functional Requirements     | Non-Functional Requirements      |
| --------------- | --------------------------- | -------------------------------- |
| Purpose         | Define what the system does | Define how well the system works |
| Focus           | Features and business logic | Quality attributes               |
| Example         | User Login                  | Login response < 200 ms          |
| User Visibility | Directly visible            | Usually indirect                 |
| Measurement     | Feature completion          | Performance and quality metrics  |

---

# Key Takeaways

## Functional Requirements

* Define system features.
* Describe user actions.
* Represent business functionality.
* Explain what the system should do.

Examples:

* Login
* Signup
* Search
* Order Placement
* Payments

## Non-Functional Requirements

* Define system quality.
* Describe how the system should behave.
* Ensure scalability, reliability, and security.

Examples:

* Scalability
* Availability
* Reliability
* Performance
* Security
* Maintainability
* Observability

## Final Note

A successful system requires both Functional and Non-Functional Requirements.

Functional Requirements ensure that the system provides the required features, while Non-Functional Requirements ensure that those features work efficiently, reliably, securely, and at scale.
