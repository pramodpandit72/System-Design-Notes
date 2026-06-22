# Message Queue

## Introduction

Modern applications often need to process millions of tasks.

Examples:

* Sending Emails
* Processing Payments
* Uploading Videos
* Sending Notifications
* Generating Reports

If every task is processed immediately, the system may become slow and overloaded.

To solve this problem, systems use **Message Queues**.

Message Queues help applications process tasks asynchronously and improve scalability.

---

# What is a Message Queue?

## Definition

A Message Queue is a communication mechanism that allows applications to send messages to a queue and process them later.

In simple words:

> A Message Queue acts as a temporary storage where tasks wait until they are processed.

---

## Basic Components

### Producer

Creates messages.

Example:

```text id="mq001"
User Places Order
```

---

### Queue

Stores messages temporarily.

```text id="mq002"
Order Queue
```

---

### Consumer

Processes messages.

```text id="mq003"
Order Processing Service
```

---

## Architecture

```text id="mq004"
Producer
    ↓
Message Queue
    ↓
Consumer
```

---

# Why Message Queues Are Needed

Without Queue:

```text id="mq005"
User
  ↓
Application
  ↓
Email Service
  ↓
SMS Service
  ↓
Payment Service
```

User waits until everything finishes.

---

With Queue:

```text id="mq006"
User
  ↓
Application
  ↓
Queue
```

Immediate response.

Background services process tasks later.

---

## Benefits

* Better scalability
* Faster response time
* Loose coupling
* Fault tolerance
* Load leveling

---

# Sync vs Async Processing

Before understanding Message Queues, we must understand synchronous and asynchronous processing.

---

# Synchronous Processing

## Definition

The client waits until the task is fully completed.

---

## Example

```text id="mq007"
User Login
    ↓
Process Request
    ↓
Return Response
```

The user waits.

---

## Visualization

```text id="mq008"
Request
   ↓
Processing
   ↓
Response
```

---

## Advantages

* Simple implementation
* Immediate result

---

## Disadvantages

* Slow for long-running tasks
* Poor scalability

---

# Asynchronous Processing

## Definition

The system accepts the request and processes it later.

---

## Example

Uploading a video:

```text id="mq009"
Upload Request
      ↓
Queue
      ↓
Response Sent
      ↓
Video Processing Later
```

---

## Visualization

```text id="mq010"
Request
   ↓
Queue
   ↓
Immediate Response

Background Processing
```

---

## Advantages

* Faster user experience
* Better scalability
* Handles spikes in traffic

---

## Disadvantages

* More complex architecture

---

# FIFO Queue

## Definition

FIFO stands for:

```text id="mq011"
First In First Out
```

Messages are processed in the same order they arrive.

---

## Example

Messages:

```text id="mq012"
Message A
Message B
Message C
```

Processing Order:

```text id="mq013"
A → B → C
```

---

## Visualization

```text id="mq014"
Front

A
B
C

Back
```

Remove from front.

---

## Use Cases

* Order Processing
* Payment Processing
* Ticket Booking Systems

Where order matters.

---

# Priority Queue

## Definition

Messages with higher priority are processed first.

Order of arrival is less important.

---

## Example

Messages:

```text id="mq015"
Low Priority  : Report Generation
High Priority : Payment Processing
Medium Priority : Notification
```

Processing Order:

```text id="mq016"
Payment
Notification
Report
```

---

## Visualization

```text id="mq017"
High Priority
      ↓
Medium Priority
      ↓
Low Priority
```

---

## Advantages

* Critical tasks processed first
* Better resource utilization

---

## Common Use Cases

* Emergency Alerts
* Payment Systems
* Healthcare Systems

---

# Pub/Sub (Publish-Subscribe)

## Definition

Pub/Sub is a messaging pattern where publishers send messages to a topic, and subscribers receive messages from that topic.

---

## Components

### Publisher

Sends messages.

### Topic

Acts as a channel.

### Subscriber

Receives messages.

---

## Architecture

```text id="mq018"
Publisher
     ↓
   Topic
 ┌───┼───┐
 ↓   ↓   ↓
S1  S2  S3
```

---

## Example

New Video Uploaded

Publisher:

```text id="mq019"
YouTube Upload Service
```

Topic:

```text id="mq020"
Video Uploaded
```

Subscribers:

```text id="mq021"
Notification Service
Recommendation Service
Analytics Service
```

All receive the same event.

---

## Advantages

* Loose coupling
* Easy scalability
* Multiple consumers

---

## Common Use Cases

* Event-driven systems
* Notifications
* Analytics pipelines

---

# Queue vs Pub/Sub

## Queue

```text id="mq022"
One Message
      ↓
One Consumer
```

---

## Pub/Sub

```text id="mq023"
One Message
      ↓
Many Subscribers
```

---

## Example

Queue:

```text id="mq024"
Order Processing
```

One worker processes the order.

---

Pub/Sub:

```text id="mq025"
User Registered
```

Many services receive the event.

---

# Push vs Pull Model

Consumers need a way to receive messages.

Two common approaches exist.

---

# Push Model

## Definition

The queue automatically sends messages to consumers.

---

## Flow

```text id="mq026"
Queue
  ↓
Consumer
```

Messages are pushed automatically.

---

## Advantages

* Low latency
* Immediate delivery

---

## Disadvantages

* Consumer may become overloaded

---

## Example

```text id="mq027"
Notification Service
```

Messages delivered instantly.

---

# Pull Model

## Definition

Consumers request messages when ready.

---

## Flow

```text id="mq028"
Consumer
   ↓
Request Message
   ↓
Queue
```

---

## Advantages

* Better control
* Consumer decides processing speed

---

## Disadvantages

* Slightly higher latency

---

## Example

```text id="mq029"
Batch Processing System
```

Workers fetch tasks when available.

---

# Push vs Pull Comparison

| Feature          | Push      | Pull              |
| ---------------- | --------- | ----------------- |
| Delivery         | Automatic | Consumer Requests |
| Latency          | Lower     | Slightly Higher   |
| Consumer Control | Less      | More              |
| Scalability      | Moderate  | Better            |

---

# Poison Messages

## Definition

A Poison Message is a message that repeatedly fails processing.

---

## Example

Suppose a message contains:

```text id="mq030"
Invalid Data
```

Consumer attempts processing:

```text id="mq031"
Attempt 1 ❌
Attempt 2 ❌
Attempt 3 ❌
Attempt 4 ❌
```

The message keeps failing.

---

## Problem

If not handled properly:

```text id="mq032"
Queue Gets Blocked
```

Other messages cannot be processed efficiently.

---

## Solution: Dead Letter Queue (DLQ)

Failed messages are moved to a separate queue.

---

## Flow

```text id="mq033"
Queue
   ↓
Failed Multiple Times
   ↓
Dead Letter Queue
```

---

## Benefits

* Prevents queue blockage
* Easier debugging
* Better reliability

---

# Duplicate Messages

## Definition

A Duplicate Message occurs when the same message is delivered more than once.

---

## Why It Happens

Example:

```text id="mq034"
Consumer Processes Message
      ↓
Acknowledgement Lost
      ↓
Queue Sends Message Again
```

The message is delivered twice.

---

## Example

```text id="mq035"
Order #101
```

Processed twice accidentally.

---

## Problems

May cause:

* Double payments
* Duplicate emails
* Repeated notifications

---

# Idempotency

## Definition

An operation is idempotent if performing it multiple times produces the same result.

---

## Example

Bad:

```text id="mq036"
Add ₹100
Add ₹100 Again
```

Result:

```text id="mq037"
₹200 Extra
```

---

Good:

```text id="mq038"
Update Status = Delivered
Update Status = Delivered Again
```

Result remains:

```text id="mq039"
Delivered
```

---

## Why It Matters

Message queues often guarantee:

```text id="mq040"
At-Least-Once Delivery
```

which means duplicates can happen.

Applications must handle duplicates safely.

---

# Popular Message Queue Systems

## RabbitMQ

Features:

* Reliable messaging
* Routing support
* FIFO queues

---

## Apache Kafka

Features:

* High throughput
* Event streaming
* Distributed architecture

---

## Amazon SQS

Features:

* Fully managed
* Scalable
* Cloud-native

---

# Real-World Example: Food Delivery App

User places an order.

---

## Flow

```text id="mq041"
User Places Order
       ↓
Order Queue
       ↓
Order Service
```

---

Then events are published:

```text id="mq042"
Order Created Event
```

Subscribers:

```text id="mq043"
Notification Service
Payment Service
Analytics Service
Restaurant Service
```

All react independently.

---

# Key Takeaways

## Message Queue

Temporary storage for messages waiting to be processed.

---

## Sync Processing

```text id="mq044"
Request
   ↓
Processing
   ↓
Response
```

User waits.

---

## Async Processing

```text id="mq045"
Request
   ↓
Queue
   ↓
Immediate Response
```

Processing happens later.

---

## FIFO Queue

```text id="mq046"
First In
First Out
```

Order preserved.

---

## Priority Queue

```text id="mq047"
High Priority
      ↓
Low Priority
```

Important tasks processed first.

---

## Pub/Sub

```text id="mq048"
Publisher
    ↓
 Topic
    ↓
Many Subscribers
```

One event can trigger multiple services.

---

## Push Model

Queue sends messages automatically.

---

## Pull Model

Consumer requests messages.

---

## Poison Messages

Messages that repeatedly fail processing.

Usually moved to:

```text id="mq049"
Dead Letter Queue
```

---

## Duplicate Messages

Same message delivered multiple times.

Prevent issues using:

```text id="mq050"
Idempotency
```

---

# Final Note

Message Queues are a critical component of modern distributed systems. They enable asynchronous processing, improve scalability, reduce system coupling, and help applications handle millions of requests efficiently. Technologies like RabbitMQ, Kafka, and Amazon SQS are widely used in large-scale systems such as Netflix, Uber, Amazon, and Instagram.
