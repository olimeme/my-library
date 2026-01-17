## Chapter 7: Transactions

## 1. Overview

Chapter 7 explores **transactions**, a fundamental abstraction that simplifies application development by grouping multiple read and write operations into a single logical unit of work.

Transactions help applications cope with:

* Partial failures
* Concurrent access
* System crashes

They provide guarantees that make systems easier to reason about, at the cost of performance and complexity.

---

## 2. What Is a Transaction?

A **transaction** is a sequence of operations that is treated as a single unit:

* Either all operations succeed
* Or none of them take effect

Transactions hide many low-level details such as crash recovery and concurrency control from application developers.

---

## 3. The ACID Properties

Transactions are commonly described using **ACID**:

### 3.1 Atomicity

* All-or-nothing execution
* Partial results are never visible
* On failure, the system rolls back changes

Atomicity is especially important in the presence of crashes.

---

### 3.2 Consistency

* Transactions move the database from one valid state to another
* All integrity constraints are preserved

Consistency is primarily an **application-level responsibility**, enforced with database constraints and logic.

---

### 3.3 Isolation

* Concurrent transactions do not interfere with each other
* Results appear as if transactions were executed serially

Isolation is often weakened in practice for performance reasons.

---

### 3.4 Durability

* Once committed, data will not be lost
* Survives crashes and restarts

Durability is achieved using:

* Write-ahead logs
* Replication
* Stable storage

---

## 4. Single-Object vs Multi-Object Operations

### 4.1 Single-Object Atomicity

Databases often guarantee atomicity for:

* Individual row updates
* Single document writes

These operations are easier to implement and scale.

---

### 4.2 Multi-Object Transactions

* Span multiple rows, documents, or keys
* More expressive but more expensive

Used for:

* Maintaining invariants
* Coordinated updates

---

## 5. Weak Isolation Levels

Strong isolation (serializability) is costly, so many systems offer weaker guarantees.

---

### 5.1 Read Committed

Guarantees:

* No dirty reads
* No dirty writes

Does **not** prevent:

* Non-repeatable reads
* Phantom reads

---

### 5.2 Snapshot Isolation

* Transactions read from a consistent snapshot
* Writes are isolated using write-write conflict detection

Prevents:

* Dirty reads
* Non-repeatable reads

Allows:

* Write skew

Used in many modern databases.

---

## 6. Serializability

**Serializability** is the strongest isolation level:

* Outcome is equivalent to some serial execution order

---

### 6.1 Implementations of Serializability

#### Two-Phase Locking (2PL)

* Locks acquired and held until commit
* Can cause blocking and deadlocks

#### Serializable Snapshot Isolation (SSI)

* Detects dangerous patterns
* Avoids blocking reads
* More complex implementation

---

## 7. Transaction Performance Trade-offs

Transactions impose costs:

* Locking overhead
* Reduced concurrency
* Increased latency

Many distributed systems:

* Avoid multi-object transactions
* Push consistency logic to applications

---

## 8. Distributed Transactions

When transactions span multiple nodes:

* Failure modes increase
* Coordination becomes expensive

### Two-Phase Commit (2PC)

Steps:

1. Prepare phase
2. Commit phase

Problems:

* Blocking if coordinator fails
* Poor scalability

---

## 9. When to Use Transactions

Transactions are valuable when:

* Data correctness is critical
* Invariants must be preserved
* Failures are common

They may be avoided when:

* High availability is required
* Latency must be minimized
* Application can tolerate anomalies

---

## 10. Trade-offs in Transaction Design

| Aspect      | Strong Transactions | Weak / No Transactions |
| ----------- | ------------------- | ---------------------- |
| Correctness | High                | Application-managed    |
| Performance | Lower               | Higher                 |
| Complexity  | Lower for app       | Lower for DB           |

Choosing the right isolation level is a key architectural decision.
