# Fault Tolerance

## Introduction

No system runs perfectly forever.

In real-world applications, failures happen all the time.

Examples:

* Hard disk crashes
* Server failures
* Network outages
* Software bugs
* Incorrect deployments
* Human mistakes

Large companies like Amazon, Netflix, Google, and Instagram expect failures to happen regularly.

Instead of trying to prevent every failure, they design systems that can continue working even when failures occur.

This concept is called **Fault Tolerance**.

---

# What is Fault Tolerance?

## Definition

Fault Tolerance is the ability of a system to continue operating correctly even when some components fail.

---

## Simple Definition

> Fault Tolerance means the system keeps working even when parts of it break.

---

## Example

Without Fault Tolerance:

```text id="ft001"
Server Failure
      ↓
Application Down
```

---

With Fault Tolerance:

```text id="ft002"
Server Failure
      ↓
Backup Server Takes Over
      ↓
Application Continues Running
```

---

## Goal of Fault Tolerance

A fault-tolerant system should:

* Detect failures
* Isolate failures
* Recover from failures
* Minimize downtime
* Prevent data loss

---

# Why Fault Tolerance is Important

Modern applications serve millions of users.

Example:

```text id="ft003"
Instagram
Netflix
Amazon
WhatsApp
```

Even a few minutes of downtime can affect:

* Revenue
* User trust
* Business operations

Therefore systems must remain available despite failures.

---

# Types of Failures

Most failures fall into four major categories:

1. Hardware Failures
2. Software Failures
3. Human Errors
4. Network Failures

This chapter focuses on the first three and how systems recover from them.

---

# Hardware Failures

## Definition

Hardware failures occur when physical components stop working.

---

## Examples

### Hard Disk Failure

```text id="ft004"
Disk Crash
      ↓
Data Unavailable
```

---

### RAM Failure

```text id="ft005"
Memory Module Failure
      ↓
Server Crash
```

---

### CPU Failure

```text id="ft006"
CPU Stops Working
      ↓
Server Unresponsive
```

---

### Power Failure

```text id="ft007"
Electricity Loss
      ↓
Machine Shutdown
```

---

### Network Card Failure

```text id="ft008"
NIC Failure
      ↓
No Network Connectivity
```

---

# Why Hardware Failures Happen

Reasons include:

* Aging hardware
* Manufacturing defects
* Overheating
* Physical damage
* Power issues

---

# Handling Hardware Failures

## Redundancy

Instead of one server:

```text id="ft009"
Application
      ↓
Server 1
```

Use multiple servers:

```text id="ft010"
Application
      ↓
 ┌──────┬──────┐
 ↓      ↓
S1      S2
```

If one fails:

```text id="ft011"
S1 ❌
S2 ✅
```

The application remains available.

---

## Replication

Store data on multiple servers.

```text id="ft012"
Primary Database
      ↓
Replica 1
Replica 2
Replica 3
```

If one database fails:

```text id="ft013"
Replica Takes Over
```

---

## Backup Systems

Maintain backup copies of important data.

```text id="ft014"
Database
      ↓
Backup Storage
```

Allows recovery after hardware loss.

---

# Software Failures

## Definition

Software failures occur when programs behave incorrectly or unexpectedly.

---

## Examples

### Application Bug

```text id="ft015"
Incorrect Code
      ↓
Unexpected Behavior
```

---

### Memory Leak

A program continuously consumes memory.

```text id="ft016"
Memory Usage
      ↑
      ↑
      ↑
Crash
```

---

### Infinite Loop

```text id="ft017"
while(true)
```

CPU usage becomes extremely high.

---

### Database Bug

```text id="ft018"
Corrupted Data
```

may be generated.

---

### Dependency Failure

```text id="ft019"
Payment Service Down
```

causes other services to fail.

---

# Why Software Failures Happen

Common causes:

* Programming mistakes
* Logic errors
* Configuration mistakes
* Dependency issues
* Poor testing

---

# Handling Software Failures

## Retry Mechanism

Temporary failures can often be fixed by retrying.

---

Example:

```text id="ft020"
Request Failed
      ↓
Retry
      ↓
Success
```

---

## Circuit Breaker

If a service repeatedly fails:

```text id="ft021"
Service Down
```

stop sending requests temporarily.

---

Visualization:

```text id="ft022"
Request
   ↓
Circuit Breaker
   ↓
Blocked
```

Prevents cascading failures.

---

## Monitoring

Continuously track:

* CPU usage
* Memory usage
* Error rates
* Response times

---

Example:

```text id="ft023"
Error Rate ↑
      ↓
Alert Generated
```

---

## Automated Restart

If an application crashes:

```text id="ft024"
Crash
  ↓
Restart Automatically
```

Tools like containers and orchestration platforms commonly do this.

---

# Human Errors

## Definition

Human errors are failures caused by mistakes made by people.

---

## Examples

### Accidental Data Deletion

```text id="ft025"
DELETE FROM Users;
```

executed accidentally.

---

### Wrong Configuration

```text id="ft026"
Incorrect Database URL
```

Application cannot connect.

---

### Bad Deployment

```text id="ft027"
Buggy Version Released
```

causing system failure.

---

### Server Shutdown

```text id="ft028"
Production Server Stopped
```

by mistake.

---

### Security Misconfiguration

```text id="ft029"
Public Access Enabled
```

exposing sensitive data.

---

# Why Human Errors Are Common

Humans make mistakes because of:

* Stress
* Lack of experience
* Miscommunication
* Manual processes
* Time pressure

---

# Reducing Human Errors

## Automation

Instead of manual tasks:

```text id="ft030"
Human Action
```

use:

```text id="ft031"
Automated Scripts
```

---

## Access Control

Limit who can perform critical operations.

Example:

```text id="ft032"
Read Access
Write Access
Admin Access
```

---

## Code Reviews

Before deployment:

```text id="ft033"
Developer
      ↓
Code Review
      ↓
Production
```

Mistakes are caught early.

---

## Testing

Use:

* Unit Tests
* Integration Tests
* End-to-End Tests

to reduce deployment failures.

---

## Rollback Mechanism

If deployment fails:

```text id="ft034"
New Version ❌
      ↓
Rollback
      ↓
Previous Version ✅
```

---

# Recovery

## Definition

Recovery is the process of restoring a system after a failure.

---

## Goal

Return the system to normal operation as quickly as possible.

---

# Recovery Methods

## Backup Restore

```text id="ft035"
Database Lost
      ↓
Restore Backup
```

---

## Failover

Automatically switch to another server.

```text id="ft036"
Primary Server ❌
      ↓
Backup Server ✅
```

---

## Replication Recovery

Replica becomes the new primary.

```text id="ft037"
Leader Failure
      ↓
Replica Promoted
```

---

## Service Restart

```text id="ft038"
Crash
  ↓
Restart
```

---

# Reliability

## Definition

Reliability measures how consistently a system performs its intended function.

---

## Simple Definition

> A reliable system works correctly for long periods without failure.

---

# Characteristics of Reliable Systems

## Availability

System remains accessible.

```text id="ft039"
Service Online
```

---

## Durability

Data is not lost.

```text id="ft040"
Data Written
      ↓
Data Preserved
```

---

## Fault Tolerance

Failures do not stop the system.

---

## Recoverability

System can recover quickly.

---

# Measuring Reliability

Common metrics include:

---

## Uptime

Percentage of time the system is available.

Example:

```text id="ft041"
99.9% Uptime
```

---

## MTBF

### Mean Time Between Failures

Average operating time before failure.

Higher is better.

---

## MTTR

### Mean Time To Recovery

Average time required to recover after failure.

Lower is better.

---

# Example

```text id="ft042"
Failure
   ↓
Recover in 2 Minutes
```

Better than:

```text id="ft043"
Failure
   ↓
Recover in 2 Hours
```

---

# Real-World Example: Netflix

Netflix runs on thousands of servers.

Failures happen daily:

```text id="ft044"
Server Failure
Network Failure
Software Failure
```

---

Netflix uses:

* Replication
* Redundancy
* Monitoring
* Automatic Recovery

to remain available.

Users often never notice failures happening behind the scenes.

---

# Fault Tolerance Techniques Summary

| Technique       | Purpose                      |
| --------------- | ---------------------------- |
| Replication     | Multiple copies of data      |
| Redundancy      | Extra servers/components     |
| Backups         | Recover lost data            |
| Monitoring      | Detect problems              |
| Retry Mechanism | Handle temporary failures    |
| Circuit Breaker | Prevent cascading failures   |
| Failover        | Switch to healthy systems    |
| Rollback        | Recover from bad deployments |

---

# Key Takeaways

## Fault Tolerance

Ability of a system to continue operating despite failures.

---

## Hardware Failures

Examples:

* Disk failure
* CPU failure
* RAM failure
* Power failure

Solution:

```text id="ft045"
Replication
Redundancy
Backups
```

---

## Software Failures

Examples:

* Bugs
* Crashes
* Memory leaks

Solution:

```text id="ft046"
Retries
Monitoring
Circuit Breakers
```

---

## Human Errors

Examples:

* Wrong deployment
* Data deletion
* Misconfiguration

Solution:

```text id="ft047"
Automation
Testing
Code Reviews
Access Control
```

---

## Recovery

Methods:

```text id="ft048"
Backup Restore
Failover
Restart
Replication
```

---

## Reliability

Measures how consistently the system works.

Important metrics:

```text id="ft049"
Uptime
MTBF
MTTR
```

---

# Final Note

Fault Tolerance is a core principle of System Design. Failures are unavoidable in large-scale systems, so successful architectures are designed to detect failures, recover quickly, and continue serving users. By using redundancy, replication, monitoring, backups, and automated recovery mechanisms, modern applications achieve high reliability and availability even in the presence of hardware failures, software bugs, and human mistakes.
