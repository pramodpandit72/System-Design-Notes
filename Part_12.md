# CAP Theorem

## Introduction

When an application runs on a single server, maintaining data consistency is relatively simple.

However, modern applications like:

* Instagram
* Netflix
* Amazon
* Facebook
* WhatsApp

run on multiple servers distributed across different locations.

In distributed systems, network failures can happen at any time.

Examples:

* Server crashes
* Network outages
* Data center failures
* Communication delays

Because of these issues, distributed systems cannot guarantee everything at the same time.

This is where the **CAP Theorem** comes in.

---

# What is CAP Theorem?

## Definition

CAP Theorem states that:

> A distributed system can guarantee only two out of the following three properties at the same time:

* Consistency (C)
* Availability (A)
* Partition Tolerance (P)

---

## Visualization

```text
        CAP Theorem

           C
          / \
         /   \
        /     \
       A-------P
```

A distributed system can choose:

```text
CA
CP
AP
```

But not all three simultaneously during a network partition.

---

# Why CAP Theorem Exists

Imagine two database servers:

```text
Server A
Server B
```

Both contain the same data.

---

Normally:

```text
Server A ↔ Server B
```

Data stays synchronized.

---

Now suppose a network failure occurs:

```text
Server A     X     Server B
```

They can no longer communicate.

This situation is called a:

```text
Network Partition
```

The system must now make a choice:

* Prioritize Consistency
* Prioritize Availability

It cannot fully guarantee both.

---

# Consistency (C)

## Definition

Consistency means every user sees the same data at the same time.

After a successful write, all future reads return the latest value.

---

## Simple Definition

> If data changes, everyone immediately sees the latest version.

---

## Example

Suppose:

```text
Account Balance = ₹1000
```

User updates it:

```text
₹1000 → ₹1500
```

---

After the update:

```text
Server A → ₹1500
Server B → ₹1500
```

Every user sees:

```text
₹1500
```

This is Consistency.

---

## Visualization

```text
Write ₹1500
      ↓
All Servers Updated
      ↓
All Reads Return ₹1500
```

---

## Why Consistency Matters

Some systems cannot tolerate stale data.

Examples:

### Banking

```text
Current Balance
```

must always be correct.

---

### Payment Systems

```text
Account Transfers
```

must show accurate information.

---

### Stock Trading

```text
Stock Prices
```

must remain consistent.

---

## Advantages

* Correct data
* Predictable behavior
* Easier reasoning

---

## Disadvantages

* May increase latency
* Can reduce availability during failures

---

# Availability (A)

## Definition

Availability means every request receives a response.

Even if some servers fail, the system continues serving users.

---

## Simple Definition

> Users always get a response, even if the response contains slightly outdated data.

---

## Example

Suppose:

```text
Server A ❌
Server B ✅
```

The system still responds:

```text
Request
   ↓
Response Returned
```

Availability is maintained.

---

## Visualization

```text
User Request
      ↓
System Responds
      ↓
Success
```

---

## Why Availability Matters

Many internet applications prioritize availability.

Examples:

### Social Media

```text
Instagram
Facebook
```

Users prefer seeing slightly old data rather than errors.

---

### Video Streaming

```text
Netflix
YouTube
```

Service should remain accessible.

---

### Messaging Apps

```text
WhatsApp
Telegram
```

Must stay online continuously.

---

## Advantages

* Better user experience
* Reduced downtime
* Higher uptime

---

## Disadvantages

* Data may become temporarily inconsistent

---

# Partition Tolerance (P)

## Definition

Partition Tolerance means the system continues operating even when communication between servers is broken.

---

## Simple Definition

> The system survives network failures between distributed servers.

---

## Example

Normally:

```text
Server A ↔ Server B
```

---

Network failure:

```text
Server A     X     Server B
```

Communication stops.

---

A partition-tolerant system continues running.

---

## Visualization

```text
Network Failure
      ↓
Servers Cannot Communicate
      ↓
System Continues Operating
```

---

## Why Partition Tolerance Matters

In distributed systems:

* Network failures are inevitable
* Data centers can become isolated
* Connections may be slow or unreliable

Therefore:

```text
Partition Tolerance
```

is almost always required.

---

## Real-World Example

Suppose:

```text
Mumbai Data Center
```

loses connection to:

```text
Delhi Data Center
```

The application should continue functioning.

---

# Understanding the Trade-Off

The most important part of CAP Theorem is understanding the trade-off.

---

# Scenario

Two servers:

```text
Server A
Server B
```

contain:

```text
Balance = ₹1000
```

---

A user updates:

```text
Balance = ₹1500
```

on Server A.

---

Immediately after:

```text
Network Partition Occurs
```

Server A cannot communicate with Server B.

---

Now another user reads data from Server B.

The system must choose:

---

# Option 1: Choose Consistency

Server B refuses to answer until synchronization happens.

---

Result:

```text
Correct Data
```

but

```text
No Response
```

for some users.

---

Properties:

```text
Consistency ✅
Availability ❌
Partition Tolerance ✅
```

This is a:

```text
CP System
```

---

# Option 2: Choose Availability

Server B returns its local value.

---

Result:

```text
Response Returned
```

but

```text
May Be Outdated
```

---

Properties:

```text
Consistency ❌
Availability ✅
Partition Tolerance ✅
```

This is an:

```text
AP System
```

---

# CA Systems

A system that guarantees:

```text
Consistency
Availability
```

without Partition Tolerance.

---

Properties:

```text
Consistency ✅
Availability ✅
Partition Tolerance ❌
```

---

## Problem

In real distributed systems:

```text
Network Failures Are Inevitable
```

Therefore true CA systems are rare in large-scale distributed environments.

---

# CP Systems

## Definition

CP systems prioritize:

```text
Consistency
Partition Tolerance
```

---

## Behavior

During network failure:

```text
Some Requests May Be Rejected
```

to maintain correctness.

---

## Visualization

```text
Network Partition
      ↓
Maintain Correct Data
      ↓
Reduce Availability
```

---

## Examples

* HBase
* ZooKeeper
* etcd

---

## Suitable For

* Banking
* Financial systems
* Inventory management

---

# AP Systems

## Definition

AP systems prioritize:

```text
Availability
Partition Tolerance
```

---

## Behavior

During network failure:

```text
Always Return Response
```

even if data may be temporarily outdated.

---

## Visualization

```text
Network Partition
      ↓
Keep Service Running
      ↓
Accept Temporary Inconsistency
```

---

## Examples

* Cassandra
* DynamoDB (certain configurations)
* CouchDB

---

## Suitable For

* Social networks
* Content platforms
* Messaging systems

---

# Eventual Consistency

Many AP systems use:

```text
Eventual Consistency
```

---

## Definition

All replicas eventually become consistent if no new updates occur.

---

## Example

```text
Server A → Updated
Server B → Old Data
```

A few seconds later:

```text
Server A → Updated
Server B → Updated
```

Consistency is eventually achieved.

---

## Real-World Example

Instagram Likes

You like a post.

Some users may see:

```text
100 Likes
```

Others may briefly see:

```text
99 Likes
```

After synchronization:

```text
100 Likes
```

for everyone.

---

# CAP Theorem Comparison

| Property            | Meaning                            |
| ------------------- | ---------------------------------- |
| Consistency         | Everyone sees the same latest data |
| Availability        | Every request gets a response      |
| Partition Tolerance | System survives network failures   |

---

# CAP Combinations

| Type | Consistency | Availability | Partition Tolerance |
| ---- | ----------- | ------------ | ------------------- |
| CA   | ✅           | ✅            | ❌                   |
| CP   | ✅           | ❌            | ✅                   |
| AP   | ❌           | ✅            | ✅                   |

---

# Real-World Examples

| System Type | Example Use Case   |
| ----------- | ------------------ |
| CP          | Banking System     |
| CP          | Payment Processing |
| AP          | Instagram Feed     |
| AP          | Facebook Timeline  |
| AP          | YouTube Views      |
| AP          | Social Media Likes |

---

# Why Partition Tolerance Is Usually Mandatory

In distributed systems:

```text
Network Failure = Guaranteed
```

Eventually every large system experiences:

* Network outages
* Packet loss
* Data center failures
* Hardware failures

Therefore most real-world systems choose between:

```text
CP
or
AP
```

instead of CA.

---

# Key Takeaways

## CAP Theorem

A distributed system can guarantee only two of:

```text
Consistency
Availability
Partition Tolerance
```

during a network partition.

---

## Consistency

```text
All Users
      ↓
See Same Data
```

Best for:

* Banking
* Payments
* Trading Systems

---

## Availability

```text
Every Request
      ↓
Gets Response
```

Best for:

* Social Media
* Streaming Platforms
* Messaging Apps

---

## Partition Tolerance

```text
Network Failure
      ↓
System Continues Running
```

Essential for distributed systems.

---

## CP Systems

```text
Consistency + Partition Tolerance
```

Sacrifice Availability.

---

## AP Systems

```text
Availability + Partition Tolerance
```

Sacrifice Immediate Consistency.

---

## Eventual Consistency

```text
Temporary Inconsistency
      ↓
Eventually Consistent
```

Common in large-scale distributed systems.

---

# Final Note

CAP Theorem is one of the most important concepts in Distributed Systems and System Design. It explains the fundamental trade-offs that every distributed system must make during network failures. Since network partitions are unavoidable, most real-world systems choose between **CP (Consistency + Partition Tolerance)** and **AP (Availability + Partition Tolerance)** depending on business requirements.
