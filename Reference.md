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

1. Data Intensive vs Compute Intensive Applications
• What makes an application data-intensive
• What makes an application compute-intensive
• Instagram architecture discussion
• Machine Learning and Rendering workloads
• CPU-bound and GPU-bound systems
• Real-world scalability concerns

2. Functional vs Non-Functional Requirements - 2
• Functional Requirements
• Scalability
• Availability
• Reliability
• Performance
• Security
• Maintainability
• Observability

3. DNS (Domain Name System) - 3
• How websites actually work
• Root Server
• TLD
• Name Server
• DNS Resolution process explained step-by-step

4. APIs and Communication - 4
• What is an API
• REST APIs
• SOAP APIs
• GraphQL
• gRPC
• WebSockets
• When and why to use each one

5. REST API Deep Dive - 5
• HTTP Methods
• GET, POST, PUT, PATCH, DELETE
• Endpoints
• JSON
• Query Parameters
• Request and Response Body
• Status Codes
• API Design Best Practices

6. SQL Databases - 6
• Relational Databases
• Tables, Rows, Columns
• Constraints
• Primary Key and Foreign Key
• Joins and Relationships
• One-to-One
• One-to-Many
• Many-to-Many

7. NoSQL Databases - 7
• Why NoSQL is needed
• Scaling challenges
• Key-Value Databases
• Document Databases
• Graph Databases
• Columnar Databases
• SQL vs NoSQL

8. Caching - 8
• Why cache is important
• Cache Hit and Cache Miss
• TTL
• Read Through Cache
• Write Through Cache
• Write Around Cache
• Write Back Cache
• Cache Eviction Policies
• LRU, LFU, FIFO, MRU, LIFO

9. Load Balancer - 9
• Why load balancers are needed
• Round Robin
• Least Connections
• Weighted Round Robin
• IP Hash
• GEO-based Routing
• Health Checks

10. Replication 
• Single Leader Replication
• Multi Leader Replication
• Leaderless Replication
• Sync vs Async Replication
• Quorum

11. Partitioning (Sharding)
• Partition by Key
• Partition by Hash
• Secondary Index Partitioning
• Hotspots and Challenges

12. CAP Theorem
• Consistency
• Availability
• Partition Tolerance
• Trade-offs in Distributed Systems

13. Message Queue
• Sync vs Async Processing
• FIFO Queue
• Priority Queue
• Pub/Sub
• Push vs Pull Model
• Poison Messages
• Duplicate Messages

14. Fault Tolerance
• Hardware Failures
• Software Failures
• Human Errors
• Recovery and Reliability

15. Monitoring and Observability
• API Monitoring
• Throughput
• Latency
• Error Rates
• Health Checks
• CPU Usage
• Memory Usage
• Disk IO
• Network IO

16. Final Case Study
System Design of a Streaming Application
• How to think while designing systems
• Video Processing Architecture
• Scalability
• Trade-offs
• Diagram Design