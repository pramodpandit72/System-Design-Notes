# Load Balancer

## Introduction

As applications grow, a single server becomes unable to handle all incoming user requests.

Imagine:

```text
10 Users  → Easy
1,000 Users → Manageable
1,000,000 Users → Difficult
```

If all requests go to one server:

* Server may become overloaded
* Response times increase
* Users experience delays
* Server may crash

To solve this problem, systems use **Load Balancers**.

Load Balancers are a fundamental component of scalable system design.

---

# What is a Load Balancer?

## Definition

A Load Balancer is a system that distributes incoming traffic across multiple servers.

In simple words:

> A Load Balancer acts like a traffic manager that sends user requests to different servers so that no single server becomes overloaded.

---

## Without Load Balancer

```text
Users
  ↓
Server 1
```

Problems:

* Single point of failure
* Overloaded server
* Poor scalability

---

## With Load Balancer

```text
Users
   ↓
Load Balancer
   ↓
 ┌─────────┬─────────┬─────────┐
 ↓         ↓         ↓
Server 1  Server 2  Server 3
```

Requests are distributed among multiple servers.

---

# Why Load Balancers are Needed

## 1. Improve Scalability

As traffic grows, more servers can be added.

```text
Server 1
Server 2
Server 3
Server 4
```

The Load Balancer distributes traffic among them.

---

## 2. Prevent Server Overload

Without balancing:

```text
Server 1 → 1000 Requests
Server 2 → 0 Requests
Server 3 → 0 Requests
```

Resources are wasted.

Load balancing distributes requests evenly.

---

## 3. Improve Availability

If one server fails:

```text
Server 1 ❌
Server 2 ✅
Server 3 ✅
```

The Load Balancer automatically sends traffic to healthy servers.

Users may not even notice the failure.

---

## 4. Improve Performance

Balanced traffic means:

* Faster responses
* Better resource utilization
* Lower latency

---

## 5. Remove Single Point of Failure

Without a Load Balancer:

```text
One Server Failure
      ↓
Entire Application Down
```

With multiple servers:

```text
One Server Failure
      ↓
Application Continues Running
```

---

# How a Load Balancer Works

## Request Flow

```text
User Request
      ↓
Load Balancer
      ↓
Select Server
      ↓
Forward Request
      ↓
Server Response
      ↓
User
```

The user does not know which server handled the request.

---

# Round Robin

## Definition

Round Robin distributes requests sequentially among servers.

Each new request goes to the next server.

---

## Example

Servers:

```text
Server 1
Server 2
Server 3
```

Requests:

```text
Request 1 → Server 1
Request 2 → Server 2
Request 3 → Server 3
Request 4 → Server 1
Request 5 → Server 2
Request 6 → Server 3
```

---

## Visualization

```text
Request 1 → S1
Request 2 → S2
Request 3 → S3
Request 4 → S1
Request 5 → S2
Request 6 → S3
```

---

## Advantages

* Simple
* Easy to implement
* Equal distribution

---

## Disadvantages

* Ignores server load
* Assumes all servers are equally powerful

---

# Least Connections

## Definition

Requests are sent to the server with the fewest active connections.

---

## Example

Current Connections:

```text
Server 1 → 100 Connections
Server 2 → 50 Connections
Server 3 → 20 Connections
```

New Request:

```text
Send to Server 3
```

because it has the least load.

---

## Visualization

```text
S1 → 100
S2 → 50
S3 → 20
       ↑
New Request
```

---

## Advantages

* Better load distribution
* Considers real server load

---

## Disadvantages

* Slightly more complex
* Requires tracking connections

---

# Weighted Round Robin

## Definition

Weighted Round Robin assigns weights to servers based on capacity.

More powerful servers receive more traffic.

---

## Example

Servers:

```text
Server 1 Weight = 3
Server 2 Weight = 2
Server 3 Weight = 1
```

Traffic Distribution:

```text
S1
S1
S1
S2
S2
S3
```

Then repeat.

---

## Visualization

```text
Server 1 → 50%
Server 2 → 33%
Server 3 → 17%
```

Approximate distribution based on weights.

---

## Advantages

* Efficient resource utilization
* Supports servers with different capacities

---

## Example Use Case

```text
Large Server → More Traffic
Small Server → Less Traffic
```

---

# IP Hash

## Definition

The user's IP address determines which server handles the request.

The same IP usually maps to the same server.

---

## Example

```text
User IP: 192.168.1.10
      ↓
Server 2
```

Every request from that IP goes to Server 2.

---

## Visualization

```text
IP A → Server 1
IP B → Server 2
IP C → Server 3
```

---

## Advantages

* Session consistency
* User stays on the same server

---

## Disadvantages

* Uneven traffic distribution
* Problems if server is removed

---

## Common Use Cases

* Session-based applications
* Shopping carts
* Legacy applications

---

# GEO-Based Routing

## Definition

Users are routed to servers based on their geographic location.

---

## Example

```text
India User
      ↓
Mumbai Server

USA User
      ↓
New York Server

Europe User
      ↓
London Server
```

---

## Visualization

```text
India  → Mumbai
USA    → New York
Europe → London
```

---

## Why It Is Useful

Users are served by nearby servers.

Benefits:

* Lower latency
* Faster response times
* Better user experience

---

## Example

Without GEO Routing:

```text
India User
      ↓
USA Server
```

High latency.

---

With GEO Routing:

```text
India User
      ↓
India Server
```

Lower latency.

---

# Health Checks

## Definition

Health Checks continuously monitor servers to determine whether they are healthy.

---

## Why Health Checks Are Needed

Suppose:

```text
Server 1 ❌ Down
Server 2 ✅ Running
Server 3 ✅ Running
```

Without health checks:

```text
Load Balancer
      ↓
Server 1
```

Users receive errors.

---

With health checks:

```text
Load Balancer
      ↓
Server 2
Server 3
```

Traffic avoids failed servers.

---

# Health Check Process

```text
Load Balancer
      ↓
Ping Server
      ↓
Healthy?
      ↓
Yes → Accept Traffic
No  → Remove From Pool
```

---

## Common Health Checks

### HTTP Check

```http
GET /health
```

Server returns:

```http
200 OK
```

meaning the server is healthy.

---

### TCP Check

Checks whether the server port is reachable.

Example:

```text
Port 80
Port 443
```

---

### Database Check

Verifies database connectivity.

---

## Example

```text
Server Healthy
      ↓
Receive Traffic

Server Unhealthy
      ↓
Stop Receiving Traffic
```

---

# Real-World Example: Instagram

Millions of users open Instagram every second.

Request Flow:

```text
Users
   ↓
Load Balancer
   ↓
 ┌─────────┬─────────┬─────────┐
 ↓         ↓         ↓
App 1     App 2     App 3
```

Benefits:

* No single server overload
* Better scalability
* High availability
* Faster responses

Without Load Balancers, large-scale applications would struggle to serve millions of users.

---

# Comparison of Load Balancing Algorithms

| Algorithm            | How It Works              | Best For               |
| -------------------- | ------------------------- | ---------------------- |
| Round Robin          | Sequential Distribution   | Equal Servers          |
| Least Connections    | Fewest Active Connections | Variable Workloads     |
| Weighted Round Robin | Based on Server Capacity  | Different Server Sizes |
| IP Hash              | Based on User IP          | Session Persistence    |
| GEO Routing          | Based on User Location    | Global Applications    |

---

# Key Takeaways

## Why Load Balancers Are Needed

* Improve scalability
* Prevent server overload
* Improve availability
* Reduce downtime
* Increase performance

---

## Round Robin

```text
S1 → S2 → S3 → Repeat
```

Simple and widely used.

---

## Least Connections

```text
New Request
      ↓
Server With Fewest Connections
```

Good for uneven workloads.

---

## Weighted Round Robin

```text
More Powerful Server
      ↓
More Traffic
```

Efficient resource utilization.

---

## IP Hash

```text
Same User IP
      ↓
Same Server
```

Useful for session persistence.

---

## GEO-Based Routing

```text
Nearest User
      ↓
Nearest Server
```

Reduces latency.

---

## Health Checks

Continuously monitor servers.

```text
Healthy → Receive Traffic
Unhealthy → Removed
```

Ensures reliability and availability.

---

# Final Note

A Load Balancer is one of the most important components in scalable system design. It distributes traffic efficiently, improves performance, increases availability, and ensures that applications continue running even when some servers fail. Almost every large-scale system, including Instagram, Netflix, Amazon, and Google, relies heavily on Load Balancers.
