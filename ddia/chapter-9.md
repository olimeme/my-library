## Chapter 9: Consistency and Consensus

## 1. Overview

Chapter 9 brings together ideas from replication, partitioning, transactions, and distributed systems to explain **consistency models** and **consensus**. It focuses on how distributed systems agree on data values and system state despite failures and uncertainty.

Key themes:

* Consistency guarantees and anomalies
* Linearizability vs weaker consistency models
* Consensus algorithms and their role

---

## 2. Consistency Guarantees

Consistency describes the **visibility and ordering of updates** as observed by clients.

It is not a single on/off property but a spectrum of guarantees.

---

## 3. Linearizability (Strong Consistency)

### 3.1 Definition

**Linearizability** means:

* Each operation appears to take effect at a single point in time
* Operations respect real-time ordering

Clients see the system as if there were only one copy of the data.

---

### 3.2 Properties

* Very intuitive for developers
* Simplifies reasoning about correctness
* Stronger than serializability for single-object operations

---

### 3.3 Implementing Linearizability

Common techniques:

* Single-leader replication
* Synchronous replication
* Consensus protocols

Costs:

* Higher latency
* Reduced availability under network partitions

---

## 4. Weaker Consistency Models

### 4.1 Eventual Consistency

* Replicas converge over time
* No guarantee on when convergence occurs

Often paired with application-level conflict resolution.

---

### 4.2 Causal Consistency

Guarantees that:

* Causally related operations are seen in the same order by all nodes
* Concurrent operations may be seen in different orders

Stronger than eventual consistency but weaker than linearizability.

---

### 4.3 Read-After-Write and Session Guarantees

Common session guarantees:

* Read-after-write consistency
* Monotonic reads
* Writes-follow-reads

Improve user experience without full strong consistency.

---

## 5. The CAP Theorem

CAP states that in the presence of a **network partition**, a system must choose between:

* **Consistency** (linearizability)
* **Availability** (every request receives a response)

Partition tolerance is assumed in distributed systems.

CAP is about **trade-offs during failures**, not normal operation.

---

## 6. Ordering and Coordination

Distributed systems often need to:

* Agree on event ordering
* Elect leaders
* Serialize access to shared resources

This requires coordination mechanisms.

---

## 7. Consensus

### 7.1 What Is Consensus?

Consensus means:

* All non-faulty nodes agree on the same value
* The agreed value was proposed by some node
* Once decided, the value does not change

Consensus is fundamental to building reliable distributed systems.

---

### 7.2 Why Consensus Is Hard

Challenges include:

* Unreliable networks
* Process crashes
* Clock uncertainty
* Partial failures

The FLP result shows that consensus is impossible in a purely asynchronous system with failures.

---

## 8. Consensus Algorithms

### 8.1 Two-Phase Commit vs Consensus

* 2PC ensures atomic commit
* Not fault-tolerant to coordinator failure
* Does not solve consensus

---

### 8.2 Paxos

Characteristics:

* Highly fault-tolerant
* Complex and hard to implement
* Forms the theoretical foundation for many systems

---

### 8.3 Raft

Designed to be:

* Easier to understand than Paxos
* Practical and widely adopted

Key components:

* Leader election
* Log replication
* Safety guarantees

Used in:

* etcd
* Consul
* Kubernetes

---

### 8.4 Zab

* Used by ZooKeeper
* Similar goals to Raft
* Focused on ordered log replication

---

## 9. Using Consensus in Practice

Consensus is often used to:

* Manage cluster membership
* Perform leader election
* Store configuration and metadata

Examples:

* Distributed locks
* Coordination services

Consensus is usually **not** used for high-volume data storage due to performance costs.

---

## 10. Consistency vs Availability Trade-offs

| Goal              | Strong Consistency | High Availability |
| ----------------- | ------------------ | ----------------- |
| Latency           | Higher             | Lower             |
| Failure tolerance | Lower              | Higher            |
| Complexity        | Lower for apps     | Higher for apps   |
