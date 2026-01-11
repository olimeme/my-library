## Chapter 5: Replication

## 1. Overview

Chapter 5 examines **replication**, the process of keeping copies of the same data on multiple machines. Replication is used to:

* Increase availability
* Improve read performance
* Reduce latency
* Provide fault tolerance

Replication introduces complexity, especially around **consistency** and **failure handling**.

---

## 2. Reasons for Replication

### 2.1 High Availability

* Replicas allow the system to continue operating when some nodes fail
* Especially important for user-facing, always-on systems

### 2.2 Scalability

* Read requests can be distributed across replicas
* Write scalability is more challenging

### 2.3 Low Latency

* Replicas placed closer to users geographically
* Reduces network round-trip time

---

## 3. Replication Models

### 3.1 Single-Leader Replication

One node is designated as the **leader (primary)**:

* All writes go to the leader
* Leader propagates changes to followers (replicas)
* Followers handle read requests

Used in many traditional databases.

#### Advantages

* Simple consistency model
* No write conflicts

#### Disadvantages

* Leader is a bottleneck
* Leader failure requires failover

---

### 3.2 Multi-Leader Replication

Multiple leaders accept writes:

* Each leader replicates changes to others
* Often used across multiple data centers

#### Advantages

* Better write availability
* Tolerates data center outages

#### Disadvantages

* Write conflicts are possible
* Conflict resolution is complex

Conflict resolution strategies:

* Last write wins
* Application-level resolution
* Custom merge logic

---

### 3.3 Leaderless Replication

No designated leader:

* Clients write to multiple replicas
* Reads query several replicas and reconcile results

Popularized by Dynamo-style systems.

#### Quorums

* Write quorum (W)
* Read quorum (R)
* Total replicas (N)

If R + W > N, reads see the latest write (in theory).

---

## 4. Replication Lag and Consistency

Replication is often **asynchronous**, leading to **replication lag**:

* Followers may be behind the leader
* Reads from replicas may be stale

This leads to **eventual consistency** rather than strong consistency.

---

## 5. Problems with Replication Lag

### 5.1 Read-After-Write Consistency

A user expects to see their own writes.

Solutions:

* Read from leader after writes
* Track write timestamps

---

### 5.2 Monotonic Reads

Users should not see data go backward in time.

Solution:

* Always read from the same replica

---

### 5.3 Consistent Prefix Reads

Related writes should be seen in the correct order.

Important for:

* Logs
* Feeds

---

## 6. Handling Node Failures

### 6.1 Leader Failure

Steps:

* Detect failure
* Choose a new leader
* Reconfigure clients

Risks:

* Split brain
* Data loss

---

### 6.2 Follower Failure

* Followers can re-sync from leader
* May require full or partial data copy

---

## 7. Replication Implementation Details

### 7.1 Statement-Based Replication

* Replicates SQL statements
* Problems with non-deterministic queries

---

### 7.2 Write-Ahead Log (WAL) Shipping

* Replicates low-level storage changes
* Tightly coupled to storage engine

---

### 7.3 Logical (Row-Based) Replication

* Replicates changes at the row level
* More flexible
* Easier schema evolution

---

## 8. Replication Topologies

Common topologies:

* Star
* Chain
* Tree
* Circular

Topology affects:

* Latency
* Fault tolerance
* Conflict likelihood

---

## 9. Trade-offs in Replication Design

| Aspect       | Benefit         | Cost               |
| ------------ | --------------- | ------------------ |
| Availability | Fault tolerance | Weaker consistency |
| Performance  | Faster reads    | Replication lag    |
| Simplicity   | Single leader   | Bottleneck         |

Replication always involves balancing consistency, availability, and complexity.

---

## 10. Summary of Chapter 5

Chapter 5 covers:

* Why replication is used
* Leader-based, multi-leader, and leaderless models
* Consistency issues caused by replication lag
* Failure handling and replication internals

Replication is a foundational technique for building resilient, distributed data systems—but it introduces unavoidable trade-offs.
