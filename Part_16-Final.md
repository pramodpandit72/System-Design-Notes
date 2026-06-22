# Final Case Study: System Design of a Streaming Application

## Introduction

In this final case study, we will design a video streaming platform similar to:

* YouTube
* Netflix
* Disney+ Hotstar
* Amazon Prime Video

The goal is not to memorize architecture diagrams.

The goal is to learn:

```text
How System Designers Think
```

When designing any large-scale system.

---

# Step 1: Understand the Problem

Before designing anything, always ask:

```text
What are we building?
```

For a streaming platform, users should be able to:

* Upload videos
* Watch videos
* Search videos
* Like videos
* Comment on videos
* Receive recommendations

---

# Functional Requirements

## Users Can

* Register/Login
* Upload videos
* Watch videos
* Search videos
* Like videos
* Comment on videos
* Subscribe to channels

---

# Non-Functional Requirements

The system should be:

* Scalable
* Highly Available
* Reliable
* Fault Tolerant
* Fast

---

# Step 2: Estimate Scale

Large systems require capacity planning.

Example:

```text
100 Million Users
```

Assume:

```text
10 Million Daily Active Users
```

---

## Video Uploads

Suppose:

```text
500,000 Videos Uploaded Daily
```

---

## Video Size

Average:

```text
100 MB
```

Storage Required Daily:

```text
500,000 × 100 MB
=
50 TB Per Day
```

Huge storage requirements.

---

# Step 3: High-Level Architecture

## Basic Flow

```text
User
 ↓
Load Balancer
 ↓
Application Servers
 ↓
Databases
```

---

## Streaming System Architecture

```text
Users
   ↓
Load Balancer
   ↓
API Servers
   ↓
Services
   ↓
Database + Cache
```

---

# Main Components

A streaming platform typically contains:

```text
API Service
User Service
Video Service
Search Service
Recommendation Service
Storage System
CDN
Database
Cache
Message Queue
```

---

# High-Level Diagram

```text
                 Users
                    ↓
             Load Balancer
                    ↓
              API Servers
                    ↓
      ┌────────┬────────┬────────┐
      ↓        ↓        ↓
 User Service Video Service Search Service
      ↓        ↓        ↓
   Database  Storage   Search DB
```

---

# How to Think While Designing Systems

This is the most important part of System Design.

Never start with databases.

Always think in this order:

---

## Step 1

```text
Requirements
```

What should the system do?

---

## Step 2

```text
Scale
```

How many users?

How much traffic?

---

## Step 3

```text
Core Components
```

What services are needed?

---

## Step 4

```text
Data Storage
```

Where is data stored?

---

## Step 5

```text
Bottlenecks
```

What can fail?

---

## Step 6

```text
Optimization
```

Caching

Replication

CDN

Queues

---

# Video Upload Flow

When a user uploads a video:

```text
User
 ↓
Upload API
 ↓
Storage
 ↓
Video Processing Queue
```

---

# Detailed Upload Architecture

```text
User
  ↓
API Server
  ↓
Object Storage
  ↓
Message Queue
  ↓
Video Processing Workers
```

---

# Why Use a Queue?

Video processing takes time.

Tasks include:

* Encoding
* Thumbnail Generation
* Compression
* Metadata Extraction

Without a queue:

```text
User Waits
```

for processing.

---

With queue:

```text
Upload Success
      ↓
Processing Happens Later
```

Better user experience.

---

# Video Processing Architecture

After upload:

```text
Video Stored
      ↓
Message Sent To Queue
      ↓
Workers Process Video
```

---

# Processing Steps

## 1. Validation

Check:

```text
Video Format
Video Size
Video Quality
```

---

## 2. Transcoding

Convert video into multiple resolutions.

Example:

```text
1080p
720p
480p
360p
```

---

Why?

Different users have different internet speeds.

---

## 3. Thumbnail Generation

Generate preview images.

```text
Video
 ↓
Thumbnail
```

---

## 4. Metadata Extraction

Extract:

```text
Duration
Resolution
Codec
```

---

## Processing Pipeline

```text
Video Upload
      ↓
Validation
      ↓
Transcoding
      ↓
Thumbnail Generation
      ↓
Metadata Extraction
      ↓
Store Results
```

---

# Storage Design

Videos are large files.

Storing them in SQL databases is not recommended.

---

## Object Storage

Store videos in:

```text
Object Storage
```

Examples:

* Amazon S3
* Google Cloud Storage

---

## Why Object Storage?

Benefits:

* Cheap
* Durable
* Highly scalable

---

# Metadata Storage

Store information such as:

```text
Title
Description
Views
Likes
Comments
```

inside databases.

---

## Example Table

```sql
Videos
------
video_id
title
description
views
created_at
```

---

# Content Delivery Network (CDN)

## Problem

Without CDN:

```text
India User
      ↓
USA Server
```

High latency.

---

## Solution

Use CDN.

---

## CDN Flow

```text
User
 ↓
Nearest CDN Server
 ↓
Video Delivered
```

---

# Example

User in Delhi:

```text
Video Served From Delhi CDN
```

instead of:

```text
USA Data Center
```

---

# Benefits of CDN

* Faster streaming
* Lower latency
* Reduced server load

---

# Database Design

Typically multiple databases are used.

---

## User Database

Stores:

```text
Users
Profiles
Subscriptions
```

---

## Video Database

Stores:

```text
Video Metadata
```

---

## Comment Database

Stores:

```text
Comments
Replies
```

---

# Caching

Popular videos receive huge traffic.

Without cache:

```text
Every Request
      ↓
Database
```

Database becomes overloaded.

---

## With Cache

```text
Request
   ↓
Cache
   ↓
Database (Only If Needed)
```

---

# Example

Trending Video:

```text
1 Million Views
```

Cache prevents database overload.

---

# Scalability

A streaming platform must support growth.

---

# Horizontal Scaling

Instead of:

```text
Bigger Server
```

add:

```text
More Servers
```

---

## Example

```text
API Server 1
API Server 2
API Server 3
API Server 4
```

---

Load Balancer distributes traffic.

---

# Database Scaling

Methods:

```text
Replication
Sharding
Caching
```

---

# Read Replicas

```text
Primary DB
     ↓
Read Replicas
```

Reads distributed across replicas.

---

# Sharding

```text
Users A-M
      ↓
Shard 1

Users N-Z
      ↓
Shard 2
```

Distributes data.

---

# Handling Millions of Streams

Suppose:

```text
5 Million Concurrent Users
```

Challenges:

* Network bandwidth
* Storage
* Video delivery

---

Solutions:

```text
CDN
Caching
Replication
Load Balancers
```

---

# Trade-offs in Streaming Systems

Every design decision has trade-offs.

---

# Trade-off 1: Consistency vs Availability

Example:

```text
View Count
```

Should it always be exact?

---

Option 1:

```text
Strong Consistency
```

Accurate but slower.

---

Option 2:

```text
Eventual Consistency
```

Faster but slightly delayed updates.

---

Most streaming platforms choose:

```text
Eventual Consistency
```

for view counts.

---

# Trade-off 2: Cost vs Performance

More servers:

```text
Better Performance
```

but:

```text
Higher Cost
```

---

# Trade-off 3: Storage vs Quality

Higher quality videos:

```text
4K
8K
```

need more storage.

---

Lower quality:

```text
Less Storage
```

but poorer user experience.

---

# Trade-off 4: Processing Speed vs Resource Usage

More processing workers:

```text
Faster Transcoding
```

but:

```text
Higher Infrastructure Cost
```

---

# Fault Tolerance

Failures are inevitable.

---

## Example

```text
Server Crash
```

System should continue operating.

---

## Techniques

### Replication

```text
Multiple Copies Of Data
```

---

### Backup

```text
Regular Data Backups
```

---

### Failover

```text
Primary Server Fails
       ↓
Backup Takes Over
```

---

# Monitoring

Track:

```text
Latency
Throughput
Error Rate
CPU Usage
Memory Usage
```

---

Example:

```text
Latency Increased
      ↓
Alert Triggered
```

Engineers investigate.

---

# Final Architecture Diagram

```text
                    Users
                       ↓
                Load Balancer
                       ↓
                 API Servers
                       ↓
       ┌───────────┬───────────┐
       ↓           ↓           ↓
 User Service  Video Service Search Service
       ↓           ↓           ↓
    Database   Object Storage Search DB
                   ↓
             Message Queue
                   ↓
          Video Processing Workers
                   ↓
         Transcoding & Thumbnails
                   ↓
                   CDN
                   ↓
                 Users
```

---

# System Design Thinking Framework

Whenever you design any system:

```text
1. Understand Requirements
2. Estimate Scale
3. Design High-Level Architecture
4. Design Database
5. Add Caching
6. Add Load Balancers
7. Add Replication
8. Add Sharding
9. Handle Failures
10. Discuss Trade-offs
```

This framework works for:

* YouTube
* Netflix
* Instagram
* WhatsApp
* Uber
* Amazon

and almost every System Design interview.

---

# Key Takeaways

## Streaming Application

Allows users to:

```text
Upload Videos
Watch Videos
Search Videos
```

---

## Video Processing Pipeline

```text
Upload
 ↓
Queue
 ↓
Validation
 ↓
Transcoding
 ↓
Thumbnail Generation
 ↓
Storage
```

---

## Scalability

Achieved using:

```text
Load Balancers
Caching
Replication
Sharding
CDN
```

---

## Trade-offs

Common trade-offs:

```text
Consistency vs Availability
Cost vs Performance
Storage vs Quality
```

---

## System Design Approach

Always think:

```text
Requirements
      ↓
Scale
      ↓
Architecture
      ↓
Storage
      ↓
Optimization
      ↓
Trade-offs
```

---

# Final Note

System Design is not about memorizing architectures. It is about understanding requirements, identifying bottlenecks, making trade-offs, and choosing the right components. If you learn how to think through a problem step by step, you can design systems ranging from simple web applications to large-scale platforms like YouTube, Netflix, Instagram, and Amazon.
