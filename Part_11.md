# Partitioning (Sharding)

## Introduction

As applications grow, the amount of data also grows.

For example:

```text
1 Thousand Users
      ↓
1 Million Users
      ↓
100 Million Users
      ↓
1 Billion Users
```

A single database server eventually becomes unable to store and process all the data efficiently.

Problems include:

* Slow queries
* Storage limitations
* High CPU usage
* High memory usage
* Poor scalability

To solve this problem, databases use **Partitioning**, also known as **Sharding**.

---

# What is Partitioning (Sharding)?

## Definition

Partitioning (Sharding) is the process of splitting a large database into smaller pieces called partitions or shards.

Each shard stores only a portion of the total data.

---

## Simple Definition

> Sharding means dividing data across multiple database servers so that no single server stores all the data.

---

## Without Sharding

```text
                Database
                    ↓
      All Users, Orders, Products
```

Single database handles everything.

Problems:

* Storage becomes huge
* Queries become slower
* Difficult to scale

---

## With Sharding

```text
             Application
                   ↓
      ┌────────┬────────┬────────┐
      ↓        ↓        ↓
   Shard 1  Shard 2  Shard 3
```

Data is distributed across multiple servers.

---

# Why Sharding is Needed

## 1. Horizontal Scalability

Instead of upgrading one server:

```text
More RAM
More CPU
Bigger Disk
```

we add more servers.

```text
DB1
DB2
DB3
DB4
```

---

## 2. Better Performance

Smaller datasets mean:

* Faster queries
* Faster indexing
* Better response times

---

## 3. Increased Storage Capacity

Each shard stores part of the data.

```text
Shard 1 → 1 TB
Shard 2 → 1 TB
Shard 3 → 1 TB
```

Total:

```text
3 TB
```

---

## 4. Improved Availability

Failure of one shard may affect only part of the system.

Not necessarily the entire application.

---

# Partition by Key

## Definition

Data is divided based on a specific key value.

This key is called the **Partition Key** or **Shard Key**.

---

## Example

Suppose User IDs are used.

### Shard 1

```text
UserID 1 - 1000
```

### Shard 2

```text
UserID 1001 - 2000
```

### Shard 3

```text
UserID 2001 - 3000
```

---

## Visualization

```text
UserID

1 - 1000      → Shard 1
1001 - 2000   → Shard 2
2001 - 3000   → Shard 3
```

---

## Request Flow

```text
UserID = 1500
      ↓
Shard 2
```

The system directly knows where the data exists.

---

## Advantages

* Simple implementation
* Fast lookup
* Easy routing

---

## Disadvantages

* Uneven distribution possible
* Some shards may become overloaded

---

# Example

Suppose Instagram stores users by ID.

```text
User 500
      ↓
Shard 1

User 1500
      ↓
Shard 2
```

The application knows exactly which shard contains the user.

---

# Partition by Hash

## Definition

Instead of using ranges, a hash function determines the shard.

---

## Formula

```text
Shard = Hash(Key) % NumberOfShards
```

---

## Example

Assume:

```text
Total Shards = 3
```

---

### User ID 101

```text
101 % 3 = 2
```

Store in:

```text
Shard 2
```

---

### User ID 102

```text
102 % 3 = 0
```

Store in:

```text
Shard 0
```

---

### User ID 103

```text
103 % 3 = 1
```

Store in:

```text
Shard 1
```

---

## Visualization

```text
User 101 → Shard 2
User 102 → Shard 0
User 103 → Shard 1
User 104 → Shard 2
```

---

## Advantages

* Better distribution
* Avoids uneven data placement
* Reduces hotspots

---

## Disadvantages

* Harder to rebalance
* Range queries become difficult

---

## Example

Find users:

```text
UserID 1000 - 2000
```

Data may be spread across all shards.

The query must check multiple shards.

---

# Partition by Key vs Hash

| Feature       | Key Partitioning | Hash Partitioning |
| ------------- | ---------------- | ----------------- |
| Distribution  | Can be uneven    | Usually balanced  |
| Range Queries | Easy             | Difficult         |
| Simplicity    | Easy             | Moderate          |
| Hotspot Risk  | Higher           | Lower             |

---

# Secondary Index Partitioning

## Problem

Suppose users are sharded by:

```text
UserID
```

---

### Shard Layout

```text
Shard 1 → UserID 1-1000
Shard 2 → UserID 1001-2000
Shard 3 → UserID 2001-3000
```

---

Now search:

```text
Find User By Email
```

Example:

```text
rahul@gmail.com
```

---

The problem:

```text
Email is not the Shard Key
```

The system does not know where the user exists.

---

# What is Secondary Index?

## Definition

A Secondary Index is an index created on fields other than the primary shard key.

---

## Example

Primary Key:

```text
UserID
```

Secondary Index:

```text
Email
Phone Number
Username
```

---

# How Secondary Index Partitioning Works

The database maintains additional indexes.

Example:

```text
Email
   ↓
UserID
   ↓
Shard Location
```

---

## Visualization

```text
Email Search
      ↓
Secondary Index
      ↓
UserID Found
      ↓
Correct Shard Found
```

---

## Advantages

* Flexible searching
* Faster lookups on non-shard-key fields

---

## Disadvantages

* Additional storage
* Extra maintenance cost
* More complexity

---

# Example

Instagram users may be stored by:

```text
UserID
```

But users login using:

```text
Email
Username
```

Secondary indexes help locate those users quickly.

---

# Hotspots

## Definition

A Hotspot occurs when one shard receives significantly more traffic than other shards.

---

## Example

Imagine partitioning by:

```text
Country
```

---

### Shard 1

```text
USA Users
```

### Shard 2

```text
India Users
```

### Shard 3

```text
Canada Users
```

---

Traffic:

```text
USA → 1 Million Requests
India → 100 Million Requests
Canada → 50 Thousand Requests
```

---

Result:

```text
India Shard Overloaded
```

while others remain underutilized.

---

# Visualization

```text
Shard 1 → 10%
Shard 2 → 85%
Shard 3 → 5%
```

Uneven load distribution.

---

# Why Hotspots Are Dangerous

They can cause:

* Slow queries
* High latency
* Server crashes
* Poor user experience

---

# Hotspot Example

Suppose social media posts are partitioned by:

```text
Celebrity ID
```

A celebrity with:

```text
100 Million Followers
```

creates huge traffic.

That shard becomes overloaded.

---

# Challenges of Sharding

Sharding solves scalability problems but introduces new challenges.

---

# 1. Uneven Data Distribution

Some shards may store:

```text
10 GB
```

while others store:

```text
500 GB
```

This causes imbalance.

---

# 2. Hotspots

Popular users or content can overload specific shards.

---

# 3. Cross-Shard Queries

Example:

```sql
SELECT *
FROM Users
WHERE Country = 'India';
```

Data may exist across multiple shards.

The query must be executed on all shards.

---

## Visualization

```text
Query
  ↓
Shard 1
Shard 2
Shard 3
Shard 4
```

Results are merged afterward.

---

# 4. Rebalancing

Suppose:

```text
3 Shards
```

becomes:

```text
5 Shards
```

Data must be moved.

This process is called:

```text
Rebalancing
```

---

# 5. Increased Complexity

Now the system must manage:

* Routing
* Replication
* Consistency
* Failures
* Rebalancing

which makes architecture more complex.

---

# Real-World Example

## Instagram

Users may be partitioned using:

```text
UserID
```

---

Posts may be distributed across:

```text
Multiple Shards
```

---

Benefits:

* Faster performance
* Better scalability
* Reduced database load

Without sharding, handling billions of users would be extremely difficult.

---

# Comparison of Partitioning Strategies

| Strategy                     | How It Works                    | Advantage             | Disadvantage            |
| ---------------------------- | ------------------------------- | --------------------- | ----------------------- |
| Partition by Key             | Range-based distribution        | Simple                | Uneven load             |
| Partition by Hash            | Hash function decides shard     | Balanced distribution | Difficult range queries |
| Secondary Index Partitioning | Additional indexes for searches | Flexible lookups      | Extra complexity        |

---

# Key Takeaways

## Partitioning (Sharding)

* Splits a large database into smaller shards.
* Enables horizontal scaling.

---

## Partition by Key

```text
UserID Range
      ↓
Specific Shard
```

Simple and efficient.

---

## Partition by Hash

```text
Hash(Key) % NumberOfShards
```

Provides better distribution.

---

## Secondary Index Partitioning

Allows searching using:

```text
Email
Username
Phone Number
```

even when they are not shard keys.

---

## Hotspots

Occur when one shard receives excessive traffic.

Can cause:

* Slow performance
* High latency
* Server overload

---

## Sharding Challenges

* Hotspots
* Uneven distribution
* Cross-shard queries
* Rebalancing
* Increased complexity

---

# Final Note

Sharding is one of the most important techniques for scaling databases in large systems. Companies like Instagram, Facebook, Netflix, Amazon, and Uber use sharding to distribute billions of records across multiple servers. While sharding greatly improves scalability and performance, it also introduces challenges such as hotspots, cross-shard queries, and rebalancing that system designers must carefully manage.
