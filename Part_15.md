# Monitoring and Observability

## Introduction

Modern applications run on multiple servers, databases, caches, queues, and external services.

Even if a system is designed perfectly, problems can still occur:

* Slow APIs
* High CPU usage
* Memory leaks
* Database bottlenecks
* Network issues
* Service failures

To detect and solve these problems, engineers use **Monitoring** and **Observability**.

These are essential for maintaining reliable and scalable systems.

---

# What is Monitoring?

## Definition

Monitoring is the process of collecting and tracking system metrics to understand the health and performance of an application.

---

## Simple Definition

> Monitoring tells us whether the system is healthy or unhealthy.

---

## Example

A monitoring system tracks:

```text
CPU Usage
Memory Usage
API Errors
Response Time
Disk Usage
```

If something goes wrong:

```text
High CPU Usage
      ↓
Alert Generated
```

Engineers are notified immediately.

---

# What is Observability?

## Definition

Observability is the ability to understand what is happening inside a system by analyzing its outputs.

---

## Simple Definition

> Observability helps us find the root cause of problems.

---

## Example

Monitoring tells us:

```text
API Response Time Increased
```

Observability helps answer:

```text
Why did it increase?
```

Possible causes:

* Database slow
* Cache failure
* Network issue
* High CPU usage

---

# Monitoring vs Observability

| Monitoring               | Observability                            |
| ------------------------ | ---------------------------------------- |
| Detects problems         | Explains problems                        |
| Focuses on metrics       | Focuses on understanding system behavior |
| Answers "What happened?" | Answers "Why did it happen?"             |
| Alerts engineers         | Helps debugging                          |

---

# Why Monitoring and Observability Are Important

Without monitoring:

```text
System Failure
      ↓
Nobody Knows
```

---

With monitoring:

```text
System Failure
      ↓
Alert Generated
      ↓
Engineers Respond
```

---

Benefits:

* Detect issues early
* Reduce downtime
* Improve reliability
* Improve performance
* Faster troubleshooting

---

# API Monitoring

## Definition

API Monitoring tracks the health and performance of APIs.

---

## Why API Monitoring Is Important

Most modern applications communicate through APIs.

Example:

```text
Frontend
    ↓
REST API
    ↓
Database
```

If the API becomes slow:

```text
Entire Application Feels Slow
```

---

## Common API Metrics

* Throughput
* Latency
* Error Rate
* Success Rate
* Request Volume

---

# Throughput

## Definition

Throughput is the number of requests processed by a system within a specific time period.

---

## Formula

```text
Throughput = Total Requests / Time
```

---

## Example

Suppose:

```text
6000 Requests
```

processed in:

```text
60 Seconds
```

Then:

```text
Throughput = 100 Requests/Second
```

---

## Visualization

```text
100 Requests
      ↓
1 Second
```

---

## Why Throughput Matters

Higher throughput means the system can handle more users.

---

## Example

Instagram:

```text
Millions of Requests
      ↓
High Throughput Required
```

---

# Latency

## Definition

Latency is the time taken to process a request and return a response.

---

## Simple Definition

> Latency measures how fast a system responds.

---

## Example

```text
Request Sent
      ↓
200 ms
      ↓
Response Received
```

Latency:

```text
200 ms
```

---

## Visualization

```text
User
  ↓
Request
  ↓
Server
  ↓
Response
```

Time taken is latency.

---

## Types of Latency

### Low Latency

```text
50 ms
```

Fast.

---

### High Latency

```text
2000 ms
```

Slow.

---

## Why Latency Matters

Users expect fast applications.

Example:

```text
Google Search
```

should respond quickly.

---

# Error Rates

## Definition

Error Rate measures the percentage of requests that fail.

---

## Formula

```text
Error Rate =
Failed Requests / Total Requests × 100
```

---

## Example

Suppose:

```text
1000 Requests
```

and

```text
20 Failed Requests
```

Then:

```text
Error Rate = 2%
```

---

## Visualization

```text
980 Success
20 Failure
```

---

## Why Error Rates Matter

Increasing error rates indicate problems.

Examples:

* Database failure
* API crash
* Network issue

---

## Healthy System

```text
Error Rate < 1%
```

Generally considered good.

---

# Health Checks

## Definition

Health Checks determine whether a service is operating correctly.

---

## Example

A Load Balancer periodically sends:

```http
GET /health
```

---

Healthy response:

```http
200 OK
```

---

Unhealthy response:

```http
500 Internal Server Error
```

---

## Visualization

```text
Load Balancer
      ↓
Health Check
      ↓
Healthy?
```

---

## Why Health Checks Matter

They prevent traffic from reaching failed servers.

---

## Example

```text
Server 1 ❌
Server 2 ✅
Server 3 ✅
```

Traffic goes only to healthy servers.

---

# CPU Usage

## Definition

CPU Usage measures how much processing power is currently being used.

---

## Example

```text
CPU Usage = 30%
```

System is healthy.

---

```text
CPU Usage = 95%
```

System is heavily loaded.

---

## Visualization

```text
CPU Capacity
100%
```

Used:

```text
95%
```

Almost full.

---

## Why CPU Monitoring Matters

High CPU can cause:

* Slow responses
* Timeouts
* Service crashes

---

## Common Causes

* Infinite loops
* Heavy computations
* Traffic spikes

---

# Memory Usage

## Definition

Memory Usage measures how much RAM is being consumed.

---

## Example

Server RAM:

```text
16 GB
```

Used:

```text
12 GB
```

---

## Why Memory Monitoring Matters

High memory usage can lead to:

```text
Out Of Memory (OOM)
```

errors.

---

## Example

Memory Leak:

```text
1 GB
2 GB
4 GB
8 GB
16 GB
```

Eventually:

```text
Application Crash
```

---

# Disk IO

## Definition

Disk IO (Input/Output) measures read and write operations performed on storage devices.

---

## Example

Database operations:

```text
Read Data
Write Data
```

require disk access.

---

## Visualization

```text
Application
      ↓
Disk
      ↓
Read/Write
```

---

## Why Disk IO Matters

Slow disks can cause:

* Slow database queries
* Slow file uploads
* Slow application performance

---

## High Disk IO Symptoms

```text
High Latency
Slow Queries
Timeouts
```

---

# Network IO

## Definition

Network IO measures data sent and received over the network.

---

## Example

API Communication:

```text
Client
   ↓
Server
```

Data travels through the network.

---

## Metrics

### Incoming Traffic

```text
Inbound Data
```

---

### Outgoing Traffic

```text
Outbound Data
```

---

## Why Network Monitoring Matters

Network problems can cause:

* Packet loss
* Increased latency
* Failed requests

---

## Example

```text
Network Bandwidth Full
      ↓
Slow Responses
```

---

# Golden Signals

Many companies monitor four critical metrics known as Golden Signals.

---

## Latency

How fast the system responds.

---

## Traffic

Amount of incoming requests.

---

## Errors

Number of failed requests.

---

## Saturation

Resource utilization.

Examples:

```text
CPU
Memory
Disk
```

---

# Example Monitoring Dashboard

A dashboard may display:

```text
CPU Usage      : 45%
Memory Usage   : 60%
Latency        : 120 ms
Error Rate     : 0.3%
Throughput     : 500 RPS
Disk Usage     : 40%
Network Usage  : 300 Mbps
```

Engineers can quickly identify issues.

---

# Real-World Example: Instagram

Millions of users interact with Instagram every second.

Monitoring tracks:

```text
API Requests
Database Performance
CPU Usage
Memory Usage
Error Rates
```

---

If latency increases:

```text
200 ms
      ↓
3000 ms
```

Alerts are triggered.

Engineers investigate and resolve the issue before it affects more users.

---

# Common Monitoring Tools

## Prometheus

Used for collecting metrics.

---

## Grafana

Used for dashboards and visualization.

---

## Datadog

Cloud-based monitoring platform.

---

## New Relic

Application performance monitoring.

---

## ELK Stack

Used for logs and observability.

```text
Elasticsearch
Logstash
Kibana
```

---

# Key Takeaways

## Monitoring

Tracks system health using metrics.

---

## Observability

Helps understand why issues occur.

---

## API Monitoring

Tracks API performance and reliability.

---

## Throughput

```text
Requests Processed Per Second
```

Measures capacity.

---

## Latency

```text
Time Taken To Respond
```

Measures speed.

---

## Error Rate

```text
Failed Requests Percentage
```

Measures reliability.

---

## Health Checks

Determine whether services are healthy.

---

## CPU Usage

Measures processor utilization.

---

## Memory Usage

Measures RAM consumption.

---

## Disk IO

Measures storage read/write operations.

---

## Network IO

Measures network traffic.

---

## Golden Signals

```text
Latency
Traffic
Errors
Saturation
```

Most important monitoring metrics.

---

# Final Note

Monitoring and Observability are critical for operating large-scale systems. Monitoring helps detect issues through metrics and alerts, while Observability helps engineers understand and diagnose the root causes of problems. By tracking API performance, throughput, latency, error rates, CPU, memory, disk IO, and network IO, organizations can build highly reliable and scalable systems that serve millions of users efficiently.
