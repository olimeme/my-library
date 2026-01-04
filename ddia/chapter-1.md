## Chapter 1 — Reliable, Scalable, and Maintainable Applications

### What is a Data-Intensive Application?

Data-intensive applications focus on handling large amounts of data, where **data management** (not CPU) is the primary challenge.

Common building blocks:

* **Databases** — store data
* **Caches** — speed up reads
* **Search indexes** — search/filter data
* **Stream processing** — process events
* **Batch processing** — periodic large-scale computation

Most real systems combine several of these components.

---

### Three Core System Qualities

#### 1. Reliability

> The system continues to work correctly, even when things go wrong.

**Typical faults**:

* Hardware failures (disk, memory, network)
* Software bugs
* Human error (misconfiguration, bad deployments)

**Key ideas**:

* Faults are expected; failures are faults that reach users
* Design for fault tolerance
* Use redundancy and isolation

Examples:

* Replication
* Graceful degradation
* Idempotent operations

---

#### 2. Scalability

> The system can handle increased load.

**Load** can be measured by:

* Requests per second
* Number of users
* Data volume

**Performance metrics**:

* Latency (response time)
* Throughput

**Latency percentiles** (e.g., p95, p99) are more meaningful than averages.

**Scaling approaches**:

* **Vertical scaling** — bigger machine
* **Horizontal scaling** — more machines

---

#### 3. Maintainability

> The system is easy to operate, understand, and evolve.

Three design principles:

* **Operability** — easy to run and monitor
* **Simplicity** — reduce accidental complexity
* **Evolvability** — easy to change over time

Techniques:

* Clear abstractions
* Good observability
* Automation

---

### Summary

Reliable systems handle faults, scalable systems handle growth, and maintainable systems support long-term development.

---

