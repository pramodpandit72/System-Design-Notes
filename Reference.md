What is System Design?
• Understanding the mindset behind designing applications
• Alien Bank example
• Components, tasks, and trade-offs in real systems

Core Components of System Design
• Client Applications
• Backend Servers
• Databases
• Load Balancers
• Message Queues
• Monitoring and Logs

Data Intensive vs Compute Intensive Applications
• What makes an application data-intensive
• What makes an application compute-intensive
• Instagram architecture discussion
• Machine Learning and Rendering workloads
• CPU-bound and GPU-bound systems
• Real-world scalability concerns

Functional vs Non-Functional Requirements
• Functional Requirements
• Scalability
• Availability
• Reliability
• Performance
• Security
• Maintainability
• Observability

DNS (Domain Name System)
• How websites actually work
• Root Server
• TLD
• Name Server
• DNS Resolution process explained step-by-step

APIs and Communication
• What is an API
• REST APIs
• SOAP APIs
• GraphQL
• gRPC
• WebSockets
• When and why to use each one

REST API Deep Dive
• HTTP Methods
• GET, POST, PUT, PATCH, DELETE
• Endpoints
• JSON
• Query Parameters
• Request and Response Body
• Status Codes
• API Design Best Practices

SQL Databases
• Relational Databases
• Tables, Rows, Columns
• Constraints
• Primary Key and Foreign Key
• Joins and Relationships
• One-to-One
• One-to-Many
• Many-to-Many

NoSQL Databases
• Why NoSQL is needed
• Scaling challenges
• Key-Value Databases
• Document Databases
• Graph Databases
• Columnar Databases
• SQL vs NoSQL

Caching
• Why cache is important
• Cache Hit and Cache Miss
• TTL
• Read Through Cache
• Write Through Cache
• Write Around Cache
• Write Back Cache
• Cache Eviction Policies
• LRU, LFU, FIFO, MRU, LIFO

Load Balancer
• Why load balancers are needed
• Round Robin
• Least Connections
• Weighted Round Robin
• IP Hash
• GEO-based Routing
• Health Checks

Replication
• Single Leader Replication
• Multi Leader Replication
• Leaderless Replication
• Sync vs Async Replication
• Quorum

Partitioning (Sharding)
• Partition by Key
• Partition by Hash
• Secondary Index Partitioning
• Hotspots and Challenges

CAP Theorem
• Consistency
• Availability
• Partition Tolerance
• Trade-offs in Distributed Systems

Message Queue
• Sync vs Async Processing
• FIFO Queue
• Priority Queue
• Pub/Sub
• Push vs Pull Model
• Poison Messages
• Duplicate Messages

Fault Tolerance
• Hardware Failures
• Software Failures
• Human Errors
• Recovery and Reliability

Monitoring and Observability
• API Monitoring
• Throughput
• Latency
• Error Rates
• Health Checks
• CPU Usage
• Memory Usage
• Disk IO
• Network IO

Final Case Study
System Design of a Streaming Application
• How to think while designing systems
• Video Processing Architecture
• Scalability
• Trade-offs
• Diagram Design