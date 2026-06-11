# 🧩 System Design Roadmap

---

## 🧩 1. FOUNDATIONS (Why systems work at all)

These are your roots. Without this, system design becomes guesswork.

### 🔹 Networking (How systems talk)

* HTTP / HTTPS → request-response model
* REST APIs → stateless communication
* TCP vs UDP → reliability vs speed
* DNS → how domain becomes IP
* TLS/SSL → secure communication

---

### 🔹 OS & Concurrency (How backend actually runs)

* Process vs Thread → memory sharing
* Context switching → CPU cost
* Deadlocks → system freeze
* Locks, Semaphores → controlling access
* Async programming → non-blocking apps

---

### 🔹 Databases (Where data lives)

* SQL vs NoSQL → structured vs flexible
* ACID → reliability rules
* Indexing → speed optimization
* Query optimization → efficient DB usage
* Transactions → safe operations
  
---

## 🧱 2. CORE SYSTEM DESIGN (The real game starts here)

### 🔹 Scalability (Handling growth)

* Vertical → increase machine power
* Horizontal → add more machines
* Auto-scaling → dynamic scaling

---

### 🔹 Load Balancing (Traffic control)

* L4 (TCP level)
* L7 (HTTP level)

**Algorithms:**

* Round Robin
* Least Connections
* IP Hash

---

### 🔹 Caching (Speed booster)

* Client cache (browser)
* Server cache (Redis)
* CDN cache

**Eviction:**

* LRU (remove least used)
* LFU (remove least frequent)

---

## ⚖️ 3. DISTRIBUTED SYSTEM PRINCIPLES (High-level thinking)

### 🔹 Consistency Models

* Strong → always correct
* Eventual → correct after time
* Read-after-write → immediate read consistency

### 🔹 CAP Theorem

* Consistency
* Availability
* Partition tolerance

---

### 🔹 Advanced

* PACELC → latency vs consistency
* Quorum → R, W, N math
* Split-brain → cluster conflict

---

## 🗄️ 4. DATABASE SCALING (Handling big data)

### 🔹 Replication

* Master-slave
* Multi-master
* Read replicas

---

### 🔹 Sharding (Partitioning)

* Range-based
* Hash-based
* Directory-based

---

### 🔹 Storage Types

* **RDBMS** → MySQL, PostgreSQL

**NoSQL:**

* Key-value → Redis
* Document → MongoDB
* Column → Cassandra
* Graph → Neo4j

---

## ⚡ 5. PERFORMANCE OPTIMIZATION

* Latency vs Throughput
* CDN
* Compression (Gzip, Brotli)
* Connection pooling
* Lazy loading

---

## 📨 6. ASYNCHRONOUS SYSTEMS (Decoupling systems)

### 🔹 Message Queues

* Kafka
* RabbitMQ
* SQS

### 🔹 Concepts

* Pub/Sub
* Event-driven architecture
* Retry mechanism
* Dead-letter queue

---

## 🔐 7. SECURITY

* Authentication vs Authorization
* OAuth, JWT
* Rate limiting
* HTTPS
* Encryption (at rest + transit)

---

## 📦 8. API DESIGN

* REST vs GraphQL
* API versioning
* Idempotency
* Pagination
* Rate limiting

---

## 🧩 9. ARCHITECTURE

### 🔹 Monolith vs Microservices

### 🔹 Components

* API Gateway
* Service discovery
* Circuit breaker
* Service mesh

---

## ☁️ 10. DEVOPS (Your strong area 💪)

* Docker
* Kubernetes
* CI/CD
* Terraform

**Monitoring:**

* Prometheus
* Grafana

**Logging:**

* ELK stack

---

## 📊 11. OBSERVABILITY

* Logs → what happened
* Metrics → system health
* Tracing → request flow

---

## 🔄 12. RELIABILITY

* Redundancy
* Failover
* Health checks
* Chaos engineering
* Backpressure

---

## 🧮 13. SYSTEM DESIGN MATH (VERY IMPORTANT ⚠️)

* Requests per second (RPS)
* Storage calculation
* Bandwidth estimation
* Latency budget

---

## 🌍 14. CONTENT DELIVERY

* CDN
* Edge computing
* Geo-replication

---

## 🧠 15. DESIGN PATTERNS (System-level thinking)

* Caching pattern
* CQRS
* Event sourcing
* Saga pattern
* Bulkhead pattern

---

## 🧪 16. REAL SYSTEM DESIGN QUESTIONS

### 🟢 Beginner

* URL Shortener
* Rate limiter
* Pastebin

### 🟡 Intermediate

* Chat app (like WhatsApp)
* File storage (like Google Drive)
* News feed (like Facebook)

### 🔴 Advanced

* Video streaming (like Netflix)
* Ride sharing (like Uber)
* Search engine (like Google)

---

## 📚 17. ADVANCED (Top 1% Engineers)

* Distributed locks (Zookeeper)
* Consensus (Paxos, Raft)
* Leader election
* Time sync (NTP)
* Multi-region systems

---

## Summary - GFG
1. Event-Driven Architecture
2. Serverless Architecture
3. Stateful vs Stateless Systems
4. Pub/Sub Architecture & Denormalization
5. Query Optimization
6. Redis Basics Systems
7. Designing Highly Scalable Systems
8. Capacity Estimation
9. Throughput and Latency Availability
10. Reliability
11. Fault Tolerance
12. CAP Theorem
13. Consistency Models
14. Replication Strategies
15. Cold vs Warm Cache Nginx Basics HTTPS
16. TCP/IP
17. DNS
18. DNS Caching
19. WebSockets
20. Long Polling
21. REST APIs
22. API Gateway
23. RabbitMQ Basics
24. Asynchronous Processing
25. Event Streaming
26. Pub/Sub Model DRY Principle
27. KISS Principle
28. YAGNI Principle
29. Design Patterns (Factory, Singleton, Observer, Strategy) DDoS Basics Kubernetes Concepts Uber/Ola)
30. Notification System
    
