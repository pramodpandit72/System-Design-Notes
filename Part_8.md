# Caching

## Introduction

Modern applications serve millions of users every day.

Examples:

* Instagram
* YouTube
* Netflix
* Amazon
* Facebook

If every request directly goes to the database, the database can become slow and overloaded.

To solve this problem, systems use **Caching**.

Caching is one of the most important techniques used in System Design to improve performance and scalability.

---

# Why Cache is Important

## Definition

A Cache is a temporary storage layer that stores frequently accessed data so it can be retrieved much faster.

In simple words:

> Cache stores commonly used data closer to the application so it can be accessed quickly.

---

## Without Cache

```text
User Request
      ↓
Application Server
      ↓
Database
      ↓
Response
```

Every request hits the database.

Problems:

* High database load
* Slow response time
* Increased latency
* Reduced scalability

---

## With Cache

```text
User Request
      ↓
Application Server
      ↓
Cache
      ↓
Response
```

Frequently accessed data is returned directly from cache.

Benefits:

* Faster responses
* Reduced database load
* Better scalability
* Lower latency

---

## Real-World Example

Suppose a product page receives:

```text
100,000 Requests
```

for the same product every hour.

Without cache:

```text
100,000 Database Queries
```

With cache:

```text
1 Database Query
99,999 Cache Reads
```

This significantly improves performance.

---

# Cache Hit and Cache Miss

Whenever an application requests data from the cache, two situations can occur.

---

# Cache Hit

## Definition

A Cache Hit occurs when the requested data is found in the cache.

---

## Example

```text
Cache:
User:101 → Rahul
```

Request:

```text
Get User 101
```

Result:

```text
Data Found in Cache
```

This is a Cache Hit.

---

## Flow

```text
Application
      ↓
Cache
      ↓
Data Found
      ↓
Response
```

---

## Benefits

* Very fast response
* No database query
* Lower latency

---

# Cache Miss

## Definition

A Cache Miss occurs when requested data is not present in the cache.

---

## Example

```text
Get User 500
```

Cache:

```text
User 500 Not Found
```

The application must fetch data from the database.

---

## Flow

```text
Application
      ↓
Cache
      ↓
Data Not Found
      ↓
Database
      ↓
Response
      ↓
Store in Cache
```

---

## Why Cache Miss Happens

* New data
* Expired data
* Evicted data
* Server restart

---

# TTL (Time To Live)

## Definition

TTL defines how long data should remain in cache before it expires.

---

## Example

```text
User Profile Cache
TTL = 1 Hour
```

After one hour:

```text
Cache Entry Removed
```

or

```text
Cache Entry Marked Expired
```

---

## Why TTL Is Needed

Without TTL:

```text
Old Data
```

may remain in cache forever.

This can cause stale or incorrect information.

---

## Example

Suppose:

```text
Product Price = ₹1000
```

Later:

```text
Product Price = ₹900
```

If cache never expires, users may continue seeing:

```text
₹1000
```

TTL helps keep cache data fresh.

---

# Read Through Cache

## Definition

In Read Through Cache, the application always reads from the cache.

If data is missing, the cache itself fetches data from the database.

---

## Flow

```text
Application
      ↓
Cache
      ↓
Database (if needed)
      ↓
Cache Updated
      ↓
Response
```

---

## Example

```text
Get User 101
```

If data is missing:

```text
Cache
      ↓
Database
      ↓
Store in Cache
      ↓
Return Data
```

---

## Advantages

* Simplifies application logic
* Automatic cache population
* Faster future reads

---

## Disadvantages

* First request may still be slow

---

# Write Through Cache

## Definition

In Write Through Cache, data is written to both cache and database simultaneously.

---

## Flow

```text
Application
      ↓
Cache
      ↓
Database
```

---

## Example

Update User Name:

```text
User → Cache
          ↓
Database
```

Both are updated immediately.

---

## Advantages

* Cache always stays updated
* Strong consistency

---

## Disadvantages

* Slower write operations
* Every write updates two systems

---

# Write Around Cache

## Definition

In Write Around Cache, data is written directly to the database.

The cache is bypassed.

---

## Flow

```text
Write Request
      ↓
Database
```

---

## Later Read

```text
Read Request
      ↓
Cache Miss
      ↓
Database
      ↓
Store in Cache
```

---

## Advantages

* Reduces unnecessary cache entries
* Good for rarely accessed data

---

## Disadvantages

* First read may be slow

---

# Write Back Cache

## Definition

In Write Back Cache, data is first written to cache and later written to the database asynchronously.

---

## Flow

```text
Application
      ↓
Cache
      ↓
Immediate Response
      ↓
Database (Later)
```

---

## Example

```text
Update User Profile
      ↓
Cache Updated
      ↓
Response Sent
      ↓
Database Updated Later
```

---

## Advantages

* Very fast writes
* Reduced database load

---

## Disadvantages

* Risk of data loss if cache crashes before database update

---

# Comparison of Cache Writing Strategies

| Strategy      | Read Speed            | Write Speed | Consistency |
| ------------- | --------------------- | ----------- | ----------- |
| Read Through  | Fast                  | Normal      | Good        |
| Write Through | Fast                  | Slower      | Strong      |
| Write Around  | Fast After Cache Fill | Fast        | Good        |
| Write Back    | Fast                  | Very Fast   | Eventual    |

---

# Cache Eviction Policies

## Definition

Cache memory is limited.

When cache becomes full, some data must be removed.

The rules used to remove data are called Cache Eviction Policies.

---

# LRU (Least Recently Used)

## Definition

Removes the data that has not been used for the longest time.

---

## Example

Cache Size:

```text
A B C
```

Recent Access:

```text
B
C
```

Least recently used:

```text
A
```

Remove:

```text
A
```

---

## Advantages

* Works well for most applications
* Widely used

---

## Common Use Cases

* Redis
* Web Applications
* API Caching

---

# LFU (Least Frequently Used)

## Definition

Removes the item that has been accessed the fewest times.

---

## Example

```text
A → 100 accesses
B → 50 accesses
C → 2 accesses
```

Remove:

```text
C
```

---

## Advantages

* Keeps popular items longer
* Good for predictable traffic

---

## Disadvantages

* More complex than LRU

---

# FIFO (First In First Out)

## Definition

Removes the oldest item inserted into the cache.

---

## Example

Inserted Order:

```text
A
B
C
```

Remove:

```text
A
```

because it entered first.

---

## Advantages

* Simple implementation

---

## Disadvantages

* Frequently used data may get removed

---

# MRU (Most Recently Used)

## Definition

Removes the most recently accessed item.

---

## Example

Recent Access Order:

```text
A
B
C
```

Most recent:

```text
C
```

Remove:

```text
C
```

---

## Use Cases

Useful when recently used data is unlikely to be used again.

---

# LIFO (Last In First Out)

## Definition

Removes the most recently inserted item.

---

## Example

Insertion Order:

```text
A
B
C
```

Remove:

```text
C
```

because it was inserted last.

---

## Advantages

* Easy to implement

---

## Disadvantages

* Rarely used in modern caching systems

---

# Cache Eviction Policy Comparison

| Policy | Removes                    |
| ------ | -------------------------- |
| LRU    | Least Recently Used Item   |
| LFU    | Least Frequently Used Item |
| FIFO   | Oldest Inserted Item       |
| MRU    | Most Recently Used Item    |
| LIFO   | Last Inserted Item         |

---

# Real-World Example: Instagram Feed

Suppose millions of users open their feeds.

Without Cache:

```text
User
   ↓
Database
```

Every request hits the database.

---

With Cache:

```text
User
   ↓
Redis Cache
   ↓
Database (Only on Miss)
```

Benefits:

* Faster feed loading
* Reduced database traffic
* Better scalability

This is one reason why large-scale applications heavily use caching.

---

# Key Takeaways

## Why Cache Is Important

* Reduces database load
* Improves performance
* Reduces latency
* Improves scalability

---

## Cache Hit

```text
Data Found in Cache
```

Fast response.

---

## Cache Miss

```text
Data Not Found in Cache
```

Database query required.

---

## TTL

Defines how long data remains in cache.

---

## Cache Strategies

### Read Through

```text
Read → Cache → Database (if needed)
```

### Write Through

```text
Write → Cache + Database
```

### Write Around

```text
Write → Database Only
```

### Write Back

```text
Write → Cache First → Database Later
```

---

## Cache Eviction Policies

### LRU

Least Recently Used

### LFU

Least Frequently Used

### FIFO

First In First Out

### MRU

Most Recently Used

### LIFO

Last In First Out

---

## Final Note

Caching is one of the most powerful techniques in System Design. It helps applications handle millions of requests efficiently by reducing database load and providing faster access to frequently used data. Most large-scale systems use caching extensively to improve performance, scalability, and user experience.
