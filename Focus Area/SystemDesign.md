# 🏗️ System Design Master Mind Map
> **Goal:** Crack Fresher Placement Interviews (SAP, Cisco, IBM, SOTI, Foodhub, Infosys, etc.)
>
> **Learning Order**
>
> ```
> Computer Networks
>        ↓
> HTTP / HTTPS
>        ↓
> Client ↔ Server
>        ↓
> APIs
>        ↓
> Databases
>        ↓
> Caching
>        ↓
> Load Balancing
>        ↓
> Scalability
>        ↓
> Distributed Systems
>        ↓
> System Design Questions
> ```
>
> Think of System Design as **connecting multiple Computer Science subjects together**.

---

# 🌍 BIG PICTURE

```
                           SYSTEM DESIGN
                                  │
        ┌─────────────────────────┼──────────────────────────┐
        │                         │                          │
    Low Level Design         High Level Design        Distributed Systems
        │                         │                          │
        │                         │                          │
    OOP Principles         Scalability              Replication
    SOLID                  Caching                  Sharding
    Design Patterns        Load Balancer            CAP Theorem
    UML                    Databases                Consistency
```

---

# 📚 COMPLETE LEARNING ROADMAP

```
System Design

├── 1. Programming Fundamentals
│      ├── OOP
│      ├── SOLID
│      ├── Design Patterns
│      ├── Clean Code
│      └── UML
│
├── 2. Networking
│      ├── HTTP
│      ├── HTTPS
│      ├── DNS
│      ├── TCP
│      ├── UDP
│      ├── SSL
│      ├── REST API
│      └── WebSockets
│
├── 3. Databases
│      ├── SQL
│      ├── NoSQL
│      ├── Indexing
│      ├── Transactions
│      ├── ACID
│      ├── Normalization
│      ├── Replication
│      └── Sharding
│
├── 4. Caching
│      ├── Browser Cache
│      ├── Server Cache
│      ├── Redis
│      ├── LRU
│      ├── LFU
│      └── Cache Invalidation
│
├── 5. Scaling
│      ├── Vertical
│      ├── Horizontal
│      ├── Load Balancer
│      ├── Auto Scaling
│      └── CDN
│
├── 6. Distributed Systems
│      ├── CAP
│      ├── Message Queue
│      ├── Kafka
│      ├── RabbitMQ
│      ├── Event Driven
│      ├── Eventual Consistency
│      └── Consistent Hashing
│
├── 7. Authentication
│      ├── Sessions
│      ├── Cookies
│      ├── JWT
│      ├── OAuth
│      └── Rate Limiting
│
└── 8. System Design Problems
       ├── URL Shortener
       ├── Instagram
       ├── WhatsApp
       ├── Uber
       ├── Netflix
       ├── Amazon
       ├── Parking Lot
       ├── Elevator
       └── ATM
```

---

# 🧠 THE COMPLETE CONNECTION MAP

```
User
 │
 │ Types URL
 ▼
DNS
 │
 ▼
IP Address
 │
 ▼
Internet
 │
 ▼
Load Balancer
 │
 ├────────────┐
 ▼            ▼
Server 1    Server 2
 │            │
 └──────┬─────┘
        ▼
Application
 │
 ├─────────────► Redis Cache
 │                 │
 │                 ▼
 │            Cache Hit?
 │
 │ Yes
 │ │
 ▼ ▼
Return Data
 │
 │ No
 ▼
Database
 │
 ▼
SQL Query
 │
 ▼
Response
 │
 ▼
API
 │
 ▼
Client
```

Everything in System Design is simply making this pipeline:

- Faster
- Cheaper
- More Reliable
- More Scalable

---

# 🟢 MODULE 1 — NETWORKING

```
Networking

├── OSI Model
├── TCP/IP
├── DNS
├── HTTP
├── HTTPS
├── SSL/TLS
├── REST
├── WebSockets
├── Cookies
└── Sessions
```

Without networking:

❌ Client cannot communicate.

Networking is the foundation.

---

# 🟢 MODULE 2 — API DESIGN

```
Client

↓

HTTP Request

↓

REST API

↓

Business Logic

↓

Database

↓

Response
```

Concepts

- GET
- POST
- PUT
- PATCH
- DELETE

Status Codes

- 200
- 201
- 400
- 401
- 403
- 404
- 500

---

# 🟢 MODULE 3 — DATABASE

```
Application

↓

Database

├── SQL
│     ├── Tables
│     ├── Joins
│     ├── Index
│     └── ACID
│
└── NoSQL
      ├── MongoDB
      ├── Cassandra
      └── Redis
```

Questions

- Where is data stored?
- How is it retrieved?
- How can retrieval become faster?

Answer

→ Indexing

---

# 🟢 MODULE 4 — INDEXING

Without Index

```
Database

↓

Read

↓

Every Row

↓

Result
```

O(n)

---

With Index

```
Database

↓

Index

↓

Jump

↓

Result
```

Almost O(log n)

---

# 🟢 MODULE 5 — CACHING

```
User

↓

Request

↓

Cache

├── Hit
│      ↓
│   Return
│
└── Miss
        ↓
Database
        ↓
Store in Cache
```

Need to know

- Redis
- LRU
- LFU
- TTL
- Cache Invalidation

---

# 🟢 MODULE 6 — LOAD BALANCER

Without LB

```
100000 Users

↓

One Server

↓

Crash
```

With LB

```
100000 Users

↓

Load Balancer

↓

Server A

Server B

Server C
```

---

# 🟢 MODULE 7 — SCALABILITY

Vertical

```
CPU ↑

RAM ↑
```

Horizontal

```
Server 1

Server 2

Server 3

Server 4
```

Interview Question

When should we move from vertical to horizontal?

---

# 🟢 MODULE 8 — DATABASE SCALING

```
Database

↓

Replication

↓

Read Replicas

↓

Fast Reads
```

---

Sharding

```
User A-M

↓

DB1

User N-Z

↓

DB2
```

---

# 🟢 MODULE 9 — DISTRIBUTED SYSTEMS

```
Multiple Servers

↓

Need Communication

↓

Consistency

↓

CAP Theorem

↓

Fault Tolerance

↓

Availability
```

Need

- Replication
- Leader Election
- Heartbeats
- Eventual Consistency

---

# 🟢 MODULE 10 — MESSAGE QUEUE

Without Queue

```
Order

↓

Email

↓

SMS

↓

Notification

↓

Payment

↓

Inventory
```

Everything waits.

---

With Queue

```
Order

↓

Kafka

↓

Email Worker

↓

SMS Worker

↓

Inventory Worker

↓

Notification Worker
```

---

# 🟢 MODULE 11 — AUTHENTICATION

```
Login

↓

Verify User

↓

JWT

↓

API Access
```

Need

- Sessions
- Cookies
- JWT
- OAuth

---

# 🟢 MODULE 12 — LOW LEVEL DESIGN

```
LLD

├── OOP
├── SOLID
├── UML
├── Design Patterns
└── Clean Code
```

Design Patterns

```
Creational

├── Singleton
├── Factory
└── Builder

Structural

├── Adapter
└── Decorator

Behavioral

├── Observer
├── Strategy
└── Command
```

---

# 🟢 MODULE 13 — COMPLETE REQUEST FLOW

```
User

↓

DNS

↓

Load Balancer

↓

Application Server

↓

Authentication

↓

Cache

↓

Database

↓

Queue

↓

Notification

↓

Response
```

This single flow combines almost every interview topic.

---

# 🟢 MODULE 14 — SYSTEM DESIGN QUESTIONS

```
Start

↓

Requirements

↓

Estimate Users

↓

Estimate Storage

↓

API Design

↓

Database

↓

Cache

↓

Load Balancer

↓

Scaling

↓

Security

↓

Monitoring

↓

Future Improvements
```

Always follow this sequence.

---

# 🎯 INTERVIEW CONNECTION GRAPH

```
OOP
 │
 ▼
SOLID
 │
 ▼
Design Patterns
 │
 ▼
LLD
 │
 ▼
Classes
 │
 ▼
Objects
 │
 ▼
API
 │
 ▼
Database
 │
 ▼
Caching
 │
 ▼
Scaling
 │
 ▼
Distributed Systems
 │
 ▼
High Level Design
```

---

# ⭐ HIGH-ROI LEARNING ORDER (80/20)

```
Phase 1
────────
✅ OOP
✅ SOLID
✅ Design Patterns
✅ UML

Phase 2
────────
✅ HTTP
✅ REST APIs
✅ Cookies
✅ Sessions
✅ JWT

Phase 3
────────
✅ SQL
✅ NoSQL
✅ Indexing
✅ ACID
✅ Transactions

Phase 4
────────
✅ Caching
✅ Redis
✅ LRU
✅ Cache Invalidation

Phase 5
────────
✅ Load Balancer
✅ Scalability
✅ CDN
✅ Replication
✅ Sharding

Phase 6
────────
✅ Kafka
✅ RabbitMQ
✅ CAP Theorem
✅ Eventual Consistency
✅ Consistent Hashing

Phase 7
────────
✅ URL Shortener
✅ WhatsApp
✅ Instagram
✅ Uber
✅ Netflix
```

---

# 🧩 ONE-LINE MEMORY CHAIN

```
Programming
    ↓
OOP
    ↓
SOLID
    ↓
Design Patterns
    ↓
Networking
    ↓
HTTP
    ↓
REST APIs
    ↓
Authentication
    ↓
Database
    ↓
Indexing
    ↓
Caching
    ↓
Load Balancer
    ↓
Scalability
    ↓
Replication
    ↓
Sharding
    ↓
Distributed Systems
    ↓
Message Queues
    ↓
System Design Interview Problems
```

> **Golden Rule:** Every advanced system design concept ultimately answers one (or more) of these questions:
> - **How do we store data?** → Databases
> - **How do we retrieve it faster?** → Indexing & Caching
> - **How do we handle more users?** → Load Balancing & Scalability
> - **How do we keep the system reliable?** → Replication, CAP, Distributed Systems
> - **How do different parts communicate?** → APIs & Message Queues
> - **How do we write maintainable software?** → OOP, SOLID, Design Patterns, LLD
