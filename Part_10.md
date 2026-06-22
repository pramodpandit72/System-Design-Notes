# Replication

## Introduction

Modern applications cannot depend on a single database server.

If one database server fails:

```text id="a1b2c3"
Database Down
      ↓
Application Down
```

This creates:

* Downtime
* Data loss risks
* Poor availability

To solve this problem, databases use **Replication**.

Replication is one of the most important concepts in Distributed Systems and System Design.

---

# What is Replication?

## Definition

Replication is the process of maintaining copies of the same data on multiple database servers.

In simple words:

> Replication means storing the same data on multiple machines so that data remains available even if some servers fail.

---

## Example

Without Replication:

```text id="r1e2p3"
Application
      ↓
Database
```

Single point of failure.

---

With Replication:

```text id="q4w5e6"
Application
      ↓
 ┌─────────────┐
 │ Primary DB  │
 └─────────────┘
      ↓
 ┌─────┬─────┬─────┐
 ↓     ↓     ↓
Replica1 Replica2 Replica3
```

Multiple copies of data exist.

---

# Why Replication is Needed

## 1. High Availability

If one database fails:

```text id="ha001"
Replica 1 ❌
Replica 2 ✅
Replica 3 ✅
```

The system continues working.

---

## 2. Fault Tolerance

Hardware failures are common.

Replication ensures data survives failures.

---

## 3. Better Read Performance

Read requests can be distributed among replicas.

```text id="rp001"
Read Request 1 → Replica 1
Read Request 2 → Replica 2
Read Request 3 → Replica 3
```

This improves scalability.

---

## 4. Disaster Recovery

If an entire server crashes:

```text id="dr001"
Primary Server ❌
Replica Server ✅
```

Data is still available.

---

# Single Leader Replication

## Definition

In Single Leader Replication, one database server is designated as the Leader (Primary).

All write operations go through the Leader.

The Leader then replicates changes to Followers (Replicas).

---

## Architecture

```text id="sl001"
          Leader
             ↓
      ┌──────┼──────┐
      ↓      ↓      ↓
Follower1 Follower2 Follower3
```

---

## Write Operation

```text id="sl002"
User
  ↓
Leader
  ↓
Followers
```

Only the Leader accepts writes.

---

## Read Operation

```text id="sl003"
User
  ↓
Leader or Followers
```

Reads may come from replicas.

---

## Example

Suppose a user updates their profile.

```text id="sl004"
Update Name = Rahul
      ↓
Leader
      ↓
Followers Updated
```

---

## Advantages

* Simple architecture
* Strong consistency (when configured properly)
* Easy to manage

---

## Disadvantages

* Leader becomes a bottleneck
* Leader failure impacts writes
* Scaling writes is difficult

---

## Common Databases

* PostgreSQL Replication
* MySQL Replication

---

# Multi Leader Replication

## Definition

In Multi Leader Replication, multiple servers can accept write requests.

Each leader replicates changes to other leaders.

---

## Architecture

```text id="ml001"
Leader A  ↔  Leader B  ↔  Leader C
```

All leaders can accept writes.

---

## Example

Suppose:

```text id="ml002"
India Users → Leader A
USA Users → Leader B
Europe Users → Leader C
```

Each region writes to its nearest leader.

---

## Flow

```text id="ml003"
User
  ↓
Nearest Leader
  ↓
Replicate To Other Leaders
```

---

## Advantages

* Better write scalability
* Lower latency
* Regional independence

---

## Disadvantages

* Conflict resolution required
* More complex architecture
* Harder consistency management

---

## Conflict Example

Leader A:

```text id="ml004"
Name = Rahul
```

Leader B:

```text id="ml005"
Name = Aman
```

at the same time.

Now the system must decide:

```text id="ml006"
Which value wins?
```

This is called a conflict.

---

## Common Use Cases

* Global Applications
* Multi-Region Deployments
* Distributed Systems

---

# Leaderless Replication

## Definition

Leaderless Replication removes the concept of a leader entirely.

Any replica can accept reads and writes.

---

## Architecture

```text id="ll001"
Replica A
Replica B
Replica C
Replica D
```

No primary server exists.

---

## Write Operation

```text id="ll002"
User
  ↓
Multiple Replicas
```

The write is sent to multiple nodes.

---

## Read Operation

```text id="ll003"
User
  ↓
Multiple Replicas
```

The system compares responses and determines the correct value.

---

## Advantages

* No single point of failure
* High availability
* Better fault tolerance

---

## Disadvantages

* Complex consistency handling
* Conflict resolution required
* More complicated implementation

---

## Popular Databases

* Cassandra
* DynamoDB

---

# Sync vs Async Replication

After data is written to the leader, replicas must be updated.

This update can happen in two ways:

1. Synchronous Replication
2. Asynchronous Replication

---

# Synchronous Replication

## Definition

The Leader waits until replicas confirm receiving the data before responding to the user.

---

## Flow

```text id="sr001"
User
  ↓
Leader
  ↓
Replica Updated
  ↓
Success Response
```

---

## Example

```text id="sr002"
Write Data
      ↓
Leader
      ↓
Replica 1 Updated
Replica 2 Updated
      ↓
Return Success
```

---

## Advantages

* Strong consistency
* No data loss

---

## Disadvantages

* Slower writes
* Higher latency

---

# Asynchronous Replication

## Definition

The Leader responds immediately after writing locally.

Replica updates happen later.

---

## Flow

```text id="ar001"
User
  ↓
Leader
  ↓
Success Response
  ↓
Replicas Updated Later
```

---

## Example

```text id="ar002"
Write Data
      ↓
Leader
      ↓
Success Returned
      ↓
Replicas Updated Later
```

---

## Advantages

* Faster writes
* Lower latency

---

## Disadvantages

* Possible data loss
* Temporary inconsistency

---

## Example Problem

```text id="ar003"
Leader Receives Write
      ↓
Leader Crashes
      ↓
Replica Not Updated Yet
```

Data may be lost.

---

# Sync vs Async Comparison

| Feature        | Synchronous | Asynchronous |
| -------------- | ----------- | ------------ |
| Speed          | Slower      | Faster       |
| Consistency    | Strong      | Eventual     |
| Data Loss Risk | Very Low    | Possible     |
| Latency        | Higher      | Lower        |
| Availability   | Lower       | Higher       |

---

# Quorum

## Definition

A Quorum is the minimum number of replicas that must acknowledge a read or write operation before it is considered successful.

---

## Why Quorum is Needed

Suppose we have:

```text id="q001"
Replica A
Replica B
Replica C
```

If one replica fails:

```text id="q002"
Replica A ✅
Replica B ✅
Replica C ❌
```

Should the operation fail?

Not necessarily.

Quorum helps determine success.

---

# Write Quorum (W)

## Definition

The minimum number of replicas that must confirm a write.

---

## Example

```text id="q003"
Total Replicas = 3
Write Quorum = 2
```

Write succeeds when:

```text id="q004"
Replica A ✅
Replica B ✅
Replica C ❌
```

Because two acknowledgements were received.

---

# Read Quorum (R)

## Definition

The minimum number of replicas consulted during a read.

---

## Example

```text id="q005"
Read Quorum = 2
```

The system reads from two replicas and compares results.

---

# Quorum Rule

The common rule is:

```text id="q006"
R + W > N
```

Where:

```text id="q007"
R = Read Quorum
W = Write Quorum
N = Total Replicas
```

---

## Example

```text id="q008"
N = 3
R = 2
W = 2
```

Check:

```text id="q009"
2 + 2 > 3
```

True.

This helps maintain consistency.

---

# Example of Quorum

Suppose:

```text id="q010"
Replicas = 3
Write Quorum = 2
Read Quorum = 2
```

Write:

```text id="q011"
Write → Replica A
Write → Replica B
```

Success.

Later:

```text id="q012"
Read → Replica B
Read → Replica C
```

At least one replica contains the latest value.

---

# Replication Models Comparison

| Feature           | Single Leader | Multi Leader      | Leaderless |
| ----------------- | ------------- | ----------------- | ---------- |
| Write Node        | One Leader    | Multiple Leaders  | Any Node   |
| Complexity        | Low           | Medium            | High       |
| Write Scalability | Limited       | Good              | Excellent  |
| Availability      | Good          | Better            | Best       |
| Conflict Handling | Minimal       | Required          | Required   |
| Example           | MySQL         | Multi-Region Apps | Cassandra  |

---

# Real-World Example

## Instagram

Profile updates may use:

```text id="ig001"
Primary Database
      ↓
Read Replicas
```

Single Leader Replication.

---

## Global Messaging Platforms

May use:

```text id="ig002"
Multiple Regional Leaders
```

Multi Leader Replication.

---

## Large Distributed Systems

May use:

```text id="ig003"
Leaderless Architecture
```

for maximum availability.

---

# Key Takeaways

## Replication

* Creates multiple copies of data.
* Improves availability and reliability.

---

## Single Leader Replication

```text id="kt001"
Leader
   ↓
Followers
```

* Simple
* Common
* Easy to manage

---

## Multi Leader Replication

```text id="kt002"
Leader ↔ Leader ↔ Leader
```

* Multiple write nodes
* Better global scalability

---

## Leaderless Replication

```text id="kt003"
Any Node Can Read/Write
```

* No single point of failure
* High availability

---

## Synchronous Replication

* Strong consistency
* Slower writes

---

## Asynchronous Replication

* Faster writes
* Eventual consistency

---

## Quorum

```text id="kt004"
R + W > N
```

Helps maintain consistency in distributed databases.

---

# Final Note

Replication is the foundation of modern distributed databases. It ensures data remains available, scalable, and fault tolerant. Understanding Single Leader, Multi Leader, Leaderless Replication, Sync vs Async Replication, and Quorum is essential for designing reliable large-scale systems such as Instagram, Netflix, Amazon, and Google.
