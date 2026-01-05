## Chapter 3 — Storage and Retrieval

### Overview

This chapter explains **how databases store and retrieve data internally** and how storage engine design affects performance, scalability, and reliability.

Key questions:

* How is data written to disk efficiently?
* How are reads optimized?
* What trade-offs do storage engines make?

---

## Storage Engine Families

There are two dominant families of storage engines:

1. **Log-Structured Storage Engines**
2. **Page-Oriented (B-Tree–based) Storage Engines**

Most modern databases use variations or hybrids of these designs.

---

## Log-Structured Storage Engines

### Core Idea

* Data is written by **appending** to a log
* Sequential disk writes are fast
* Old data is removed via compaction

Simplified model:

```
set(key, value) → append to log
get(key) → use index to locate value
```

---

### Indexes

An **index** maps keys to locations in data files.

Purpose:

* Speed up reads

Costs:

* Extra storage
* Slower writes (index maintenance)

---

### Hash Indexes

* In-memory hash map: key → file offset
* Extremely fast lookups
* All keys must fit in memory

Used in:

* Bitcask (Riak)

Limitations:

* No efficient range queries
* Memory-bound

---

### Segment Files and Compaction

Problem:

* Log files grow indefinitely

Solution:

* Split logs into **segments**
* Periodically **compact** them

Compaction does:

* Removes obsolete values
* Merges segments

Benefits:

* Reclaims disk space
* Improves read efficiency

---

## LSM Trees (Log-Structured Merge Trees)

### Structure

* **Memtable**: in-memory sorted data
* **SSTables**: immutable, sorted on-disk files
* Background compaction merges SSTables

### Write Path

1. Write to memtable
2. Flush memtable to disk as SSTable
3. Compact older SSTables

### Read Path

* Check memtable
* Check newer SSTables first
* Continue to older SSTables if needed

---

### Advantages of LSM Trees

* High write throughput
* Sequential disk I/O
* Good compression ratios

Used in:

* LevelDB
* RocksDB
* Cassandra
* HBase

---

### Disadvantages of LSM Trees

* Read amplification
* Write amplification
* Compaction can cause latency spikes

---

## Page-Oriented Storage Engines (B-Trees)

### B-Tree Basics

* Data stored in fixed-size pages
* Pages organized in a balanced tree
* Data updated **in place**

Operations:

* Reads traverse the tree
* Writes modify pages

---

### Characteristics of B-Trees

**Pros**:

* Predictable read latency
* Excellent range queries
* Mature design

**Cons**:

* Random disk writes
* More complex concurrency handling

Used in:

* PostgreSQL
* MySQL (InnoDB)
* SQLite

---

## LSM Trees vs B-Trees

| Aspect            | LSM Tree   | B-Tree         |
| ----------------- | ---------- | -------------- |
| Write performance | Excellent  | Moderate       |
| Read performance  | Variable   | Predictable    |
| Disk I/O          | Sequential | Random         |
| Range queries     | Good       | Very good      |
| Background work   | Compaction | Page splitting |

---

## Secondary Indexes

* Indexes on non-primary attributes
* May point directly to rows or to primary keys

Challenges:

* Consistency with base data
* Increased write cost

---

## Clustered vs Non-Clustered Indexes

* **Clustered index**: data stored in index order
* **Non-clustered index**: index points elsewhere

Trade-off:

* Read efficiency vs flexibility

---

## In-Memory Databases

Characteristics:

* Data stored primarily in RAM
* Persistence via logs or snapshots

Advantages:

* Very low latency

Challenges:

* Higher cost
* Durability concerns

Examples:

* Redis
* VoltDB

---

## Transactional vs Analytical Workloads

### OLTP

* Many small reads/writes
* Low latency focus

### OLAP

* Large scans
* High throughput focus

Storage engines are usually optimized for one type.

---

## Column-Oriented Storage

Primarily used for analytics.

Key ideas:

* Store data by column instead of row
* Better compression
* Faster aggregations

Examples:

* Parquet
* ORC

---

## Summary

* Storage engine design heavily influences database behavior
* LSM trees favor write-heavy workloads
* B-trees favor read-heavy and range-query workloads
* Choose based on access patterns

---

## Key Takeaways

* Indexes improve reads but add write cost
* Compaction is essential in log-structured systems
* There is no universally optimal storage engine

---

*Based on **Designing Data-Intensive Applications** by Martin Kleppmann*
