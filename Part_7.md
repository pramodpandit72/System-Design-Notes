# NoSQL Databases

## Introduction

As applications like:

* Facebook
* Instagram
* YouTube
* Netflix
* Amazon

started serving millions and billions of users, traditional SQL databases began facing scalability challenges.

Large-scale applications needed databases that could:

* Scale horizontally
* Handle massive amounts of data
* Support flexible data structures
* Provide high availability

This led to the rise of **NoSQL Databases**.

---

# What is NoSQL?

## Definition

NoSQL stands for:

```text
Not Only SQL
```

A NoSQL database is a non-relational database designed to store and manage large volumes of data efficiently.

Unlike SQL databases, NoSQL databases do not require data to be stored in fixed tables with predefined schemas.

---

## Simple Definition

> NoSQL databases are databases designed for scalability, flexibility, and high-performance data storage.

---

## Popular NoSQL Databases

### Key-Value

* Redis
* DynamoDB

### Document

* MongoDB
* CouchDB

### Graph

* Neo4j
* Amazon Neptune

### Columnar

* Cassandra
* HBase

---

# Why NoSQL is Needed

## The Problem with Traditional SQL Databases

SQL databases work extremely well for:

* Banking systems
* ERP systems
* Hospital management systems

However, large internet companies face different challenges.

Imagine Instagram storing:

```text
2 Billion Users
100+ Million Photos Uploaded Daily
Billions of Likes
Billions of Comments
```

Handling such huge amounts of data using a single SQL server becomes difficult.

---

## Challenges Faced by SQL Databases

### 1. Massive Data Growth

Data grows faster than a single machine can handle.

Example:

```text
1 TB
10 TB
100 TB
1000 TB
```

Eventually one server becomes insufficient.

---

### 2. High Traffic

Millions of users may access the system simultaneously.

Example:

```text
Instagram Feed Requests
Messages
Likes
Comments
```

The database must handle enormous traffic.

---

### 3. Horizontal Scaling Difficulty

SQL databases traditionally scale vertically.

```text
More CPU
More RAM
Bigger Server
```

This becomes expensive.

---

### 4. Flexible Data Structures

Modern applications often store:

* Images
* Videos
* User preferences
* Activity logs
* Dynamic metadata

This data may not fit neatly into relational tables.

---

# Scaling Challenges

## Vertical Scaling

Increase resources of a single machine.

```text
4 GB RAM
     ↓
64 GB RAM
```

Advantages:

* Easy to implement

Problems:

* Expensive
* Hardware limits exist
* Single point of failure

---

## Horizontal Scaling

Add more servers.

```text
Database 1
Database 2
Database 3
Database 4
```

Advantages:

* Better scalability
* Better fault tolerance
* Lower cost at scale

Most NoSQL databases are designed for horizontal scaling.

---

# Types of NoSQL Databases

NoSQL databases are generally divided into four major categories:

1. Key-Value Databases
2. Document Databases
3. Graph Databases
4. Columnar Databases

---

# Key-Value Databases

## Definition

A Key-Value Database stores data as:

```text
Key → Value
```

The key acts as a unique identifier.

The value contains the actual data.

---

## Example

```text
user:101 → Rahul
user:102 → Aman
user:103 → Priya
```

---

## Real Example

```json
{
  "user:101": {
    "name": "Rahul",
    "age": 22
  }
}
```

---

## Visualization

```text
Key             Value
--------------------------------
user:101   →   Rahul
user:102   →   Aman
user:103   →   Priya
```

---

## Advantages

* Extremely fast
* Simple structure
* Easy horizontal scaling
* Low latency

---

## Disadvantages

* Limited querying capabilities
* Not suitable for complex relationships

---

## Common Use Cases

### Caching

```text
Redis
```

### Session Storage

```text
User Login Sessions
```

### Shopping Carts

```text
Amazon Cart
```

---

# Document Databases

## Definition

A Document Database stores data as documents.

Usually documents are stored in:

* JSON
* BSON

format.

---

## Example

```json
{
  "id": 101,
  "name": "Rahul",
  "email": "rahul@gmail.com",
  "skills": [
    "Java",
    "Spring Boot"
  ]
}
```

Each document can have a different structure.

---

## Visualization

```text
Users Collection
      ↓
Document 1
Document 2
Document 3
```

---

## Advantages

* Flexible schema
* Easy to store nested data
* Developer-friendly
* Good performance

---

## Disadvantages

* Relationships are harder than SQL

---

## Common Use Cases

### User Profiles

```json
{
  "name": "Rahul",
  "skills": ["Java", "React"]
}
```

### Product Catalogs

### Content Management Systems

### Social Media Applications

---

## Popular Database

```text
MongoDB
```

---

# Graph Databases

## Definition

Graph Databases store data as:

```text
Nodes + Relationships
```

instead of tables.

---

## Why Graph Databases Exist

Some systems are relationship-heavy.

Examples:

* Facebook Friends
* LinkedIn Connections
* Recommendation Systems

SQL joins become expensive for deeply connected data.

---

## Example

```text
Rahul
  ↓ Friend
Aman
  ↓ Friend
Priya
```

---

## Visualization

```text
Rahul
  ↔
Aman
  ↔
Priya
```

Relationships are stored directly.

---

## Advantages

* Extremely fast relationship queries
* Natural representation of networks
* Efficient recommendations

---

## Disadvantages

* Not ideal for simple CRUD systems
* Complex implementation

---

## Common Use Cases

### Social Networks

```text
Facebook
LinkedIn
```

### Recommendation Engines

```text
Netflix
Amazon
```

### Fraud Detection Systems

---

## Popular Database

```text
Neo4j
```

---

# Columnar Databases

## Definition

Columnar Databases store data by columns instead of rows.

---

## Traditional SQL Storage

```text
Row 1 → Rahul, 22, India
Row 2 → Aman, 23, India
Row 3 → Priya, 21, India
```

Stored row by row.

---

## Columnar Storage

```text
Names
------
Rahul
Aman
Priya

Ages
------
22
23
21

Country
---------
India
India
India
```

Stored column by column.

---

## Why Columnar Storage Is Useful

Suppose we only need ages.

SQL row-based database reads:

```text
Name
Age
Country
```

for every row.

Columnar database reads:

```text
Age
```

only.

This improves analytical query performance.

---

## Advantages

* Excellent for analytics
* Fast aggregation queries
* Efficient storage

---

## Disadvantages

* Not ideal for frequent updates
* Complex architecture

---

## Common Use Cases

### Data Warehouses

### Big Data Analytics

### Reporting Systems

### Real-Time Analytics

---

## Popular Databases

* Cassandra
* HBase

---

# SQL vs NoSQL

Both databases solve different problems.

Neither is universally better.

The choice depends on requirements.

---

# Data Structure

### SQL

```text
Tables
Rows
Columns
```

### NoSQL

```text
Documents
Key-Value
Graphs
Columns
```

---

# Schema

### SQL

Fixed schema.

```text
Name VARCHAR(100)
Age INT
```

must be defined beforehand.

---

### NoSQL

Flexible schema.

Different documents can have different fields.

---

# Scalability

### SQL

Traditionally scales vertically.

```text
Bigger Server
```

---

### NoSQL

Designed for horizontal scaling.

```text
More Servers
```

---

# Relationships

### SQL

Excellent support.

```text
JOINS
Foreign Keys
Relationships
```

---

### NoSQL

Limited relationship support.

Often handled at application level.

---

# Consistency

### SQL

Strong consistency.

Ideal for financial systems.

---

### NoSQL

Often prioritizes:

* Availability
* Scalability

over strict consistency.

---

# SQL vs NoSQL Comparison Table

| Feature       | SQL             | NoSQL               |
| ------------- | --------------- | ------------------- |
| Data Model    | Tables          | Multiple Models     |
| Schema        | Fixed           | Flexible            |
| Scaling       | Vertical        | Horizontal          |
| Relationships | Strong          | Limited             |
| Joins         | Supported       | Limited             |
| Consistency   | Strong          | Often Eventual      |
| Performance   | Good            | Excellent at Scale  |
| Best For      | Structured Data | Large Scale Systems |

---

# When to Use SQL

Choose SQL when:

* Data relationships are important
* Transactions are critical
* Consistency is required
* Data structure is stable

### Examples

* Banking Systems
* Payment Systems
* ERP Applications
* Hospital Systems

---

# When to Use NoSQL

Choose NoSQL when:

* Massive scalability is required
* Flexible schemas are needed
* Huge traffic is expected
* Data changes frequently

### Examples

* Instagram
* Facebook
* Netflix
* YouTube
* Uber

---

# Real-World Example

## Instagram

Different databases are used for different purposes.

### SQL Database

Stores:

```text
User Accounts
Billing Data
Transactions
```

---

### NoSQL Database

Stores:

```text
Posts
Likes
Comments
Feeds
Activity Logs
```

This combination provides both consistency and scalability.

---

# Key Takeaways

## Why NoSQL Is Needed

* Massive scale
* Flexible data structures
* High availability
* Horizontal scaling

---

## Types of NoSQL Databases

### Key-Value

```text
Key → Value
```

Examples:

* Redis
* DynamoDB

---

### Document

```text
JSON Documents
```

Examples:

* MongoDB
* CouchDB

---

### Graph

```text
Nodes + Relationships
```

Examples:

* Neo4j
* Neptune

---

### Columnar

```text
Column-Based Storage
```

Examples:

* Cassandra
* HBase

---

## SQL vs NoSQL

### SQL

Best for:

* Transactions
* Relationships
* Consistency

### NoSQL

Best for:

* Scalability
* High traffic
* Flexible data

---

## Final Note

NoSQL databases were created to solve the scalability and flexibility challenges of modern internet applications. Today, most large-scale systems use a combination of SQL and NoSQL databases, choosing the right database based on the specific problem being solved.
