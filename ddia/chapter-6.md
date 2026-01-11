## Chapter 6: Partitioning

## 1. Overview

Chapter 6 focuses on **partitioning** (also called sharding): splitting a large dataset into smaller subsets that can be stored and processed on multiple machines. Partitioning is essential for:

* Scalability
* High throughput
* Managing large datasets

Partitioning complements replication but solves a different problem: **scaling data volume and write load**.

---

## 2. Why Partition Data?

Primary motivations:

* **Scalability**: distribute data and load across nodes
* **Performance**: parallelize queries
* **Manageability**: avoid single-node bottlenecks

A well-partitioned system ensures that no single node becomes overloaded.

---

## 3. Partitioning vs Replication

* **Replication**: keeps copies of the same data on multiple nodes
* **Partitioning**: splits distinct subsets of data across nodes

In practice, systems often use **both**:

* Each partition is replicated for fault tolerance

---

## 4. Key-Based Partitioning

### 4.1 Partitioning by Key Range

Data is partitioned based on a **range of keys**:

* Example: A–F, G–M, N–Z

#### Advantages

* Efficient range queries
* Data locality for related keys

#### Disadvantages

* Risk of **hot partitions** if access is skewed

---

### 4.2 Partitioning by Hash of Key

* A hash function maps keys to partitions
* Even distribution of data

#### Advantages

* Reduces hotspots
* Good load balancing

#### Disadvantages

* Poor support for range queries
* Loss of key ordering

---

## 5. Secondary Indexes and Partitioning

### 5.1 Local Secondary Indexes

* Each partition maintains its own secondary indexes
* Queries must be sent to **all partitions**

Also known as **scatter/gather** queries.

---

### 5.2 Global Secondary Indexes

* Index spans all partitions
* Index itself must be partitioned

#### Trade-offs

* Faster reads
* More complex writes
* Additional consistency challenges

---

## 6. Rebalancing Partitions

As data volume and load change, partitions must be redistributed.

Goals of rebalancing:

* Even load distribution
* Minimal data movement
* Continued availability

---

### 6.1 Fixed Number of Partitions

* Partitions created in advance
* Assigned to nodes dynamically

Used in systems like:

* Elasticsearch
* Riak

---

### 6.2 Dynamic Partitioning

* Split partitions as they grow
* Often used with key-range partitioning

Example:

* HBase
* MongoDB

---

### 6.3 Partitioning Proportional to Nodes

* Number of partitions scales with cluster size
* Uses **virtual nodes**

Common in hash-based systems like Cassandra.

---

## 7. Request Routing

Clients need to know **which node owns a partition**.

Routing approaches:

* Client-side routing
* Proxy-based routing
* Coordinator nodes

Metadata about partition ownership must be kept consistent.

---

## 8. Handling Skew and Hotspots

Skew occurs when:

* Some partitions receive more traffic than others

Mitigation strategies:

* Use hashing
* Add random prefixes
* Split hot partitions
* Application-level load balancing

---

## 9. Partitioning and Transactions

Challenges:

* Transactions spanning multiple partitions
* Increased latency
* Higher failure probability

Many systems:

* Avoid cross-partition transactions
* Provide limited transactional guarantees

---

## 10. Trade-offs in Partitioned Systems

| Aspect      | Benefit         | Cost                   |
| ----------- | --------------- | ---------------------- |
| Scalability | High throughput | Complex coordination   |
| Performance | Parallelism     | Scatter/gather queries |
| Flexibility | Elastic growth  | Operational overhead   |

Partitioning increases scalability but adds significant complexity.

---

## 11. Summary of Chapter 6

Chapter 6 explains:

* Why partitioning is essential for large-scale systems
* Key-based and hash-based partitioning strategies
* Challenges with secondary indexes and rebalancing
* How partitioning affects routing, transactions, and performance

Effective partitioning is a cornerstone of scalable, distributed data systems.
