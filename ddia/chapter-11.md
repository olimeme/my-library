## Chapter 11: Stream Processing

## 1. Overview

Chapter 11 focuses on **stream processing**, which handles data **continuously as it arrives**, rather than in large offline batches. Stream processing is essential for applications that require:

* Low latency
* Real-time insights
* Continuous computation

Streams complement batch processing and are often used together in modern data architectures.

---

## 2. Batch Processing vs Stream Processing

Key differences:

| Aspect         | Batch Processing | Stream Processing   |
| -------------- | ---------------- | ------------------- |
| Data           | Finite, bounded  | Infinite, unbounded |
| Latency        | High             | Low                 |
| Processing     | Periodic         | Continuous          |
| Fault handling | Recompute        | Checkpoint / replay |

Stream processing treats data as an **unbounded sequence of events**.

---

## 3. Transmitting Event Streams

### 3.1 Message Brokers

Streams are often transmitted via **message brokers** that:

* Persist messages
* Allow multiple consumers
* Decouple producers from consumers

Examples:

* Kafka
* Pulsar
* Kinesis

---

### 3.2 Direct Messaging Systems

Older systems:

* JMS
* AMQP-based queues

Limitations:

* Poor scalability
* Limited message retention

---

## 4. Message Broker vs Database

Differences:

* Brokers are optimized for **append-only writes**
* Databases support random reads and complex queries

Modern systems increasingly blur this boundary.

---

## 5. Stream Processing Concepts

### 5.1 Events

An **event** represents something that happened at a point in time:

* User click
* Sensor reading
* Transaction

Events are immutable once written.

---

### 5.2 Event Time vs Processing Time

* **Event time**: when the event actually occurred
* **Processing time**: when the system processes the event

Differences arise due to:

* Network delays
* Retries
* Out-of-order delivery

---

## 6. Windowing

Since streams are infinite, computations are done over **windows**.

Common window types:

* Tumbling windows
* Sliding windows
* Session windows

Windowing allows aggregation over bounded subsets of a stream.

---

## 7. Stream Joins

Joining streams is challenging because:

* Data arrives continuously
* Events may be delayed or missing

Approaches:

* Windowed joins
* Stream–table joins

---

## 8. Fault Tolerance in Stream Processing

Stream processors must handle failures without losing data.

Techniques:

* Message replay
* Checkpointing operator state
* Exactly-once or at-least-once semantics

---

## 9. Delivery Semantics

### At-Most-Once

* Messages may be lost
* No duplicates

### At-Least-Once

* Messages are not lost
* Duplicates possible

### Exactly-Once

* Messages processed once
* Hardest to implement

Exactly-once semantics often rely on idempotent operations and transactional writes.

---

## 10. Stateful Stream Processing

Modern stream processors maintain **state**, such as:

* Aggregates
* Windows
* Join buffers

State is:

* Periodically checkpointed
* Restored on failure

---

## 11. Stream Processing Frameworks

Popular frameworks:

* Apache Flink
* Kafka Streams
* Spark Structured Streaming

They provide:

* High-level APIs
* Fault tolerance
* State management

---

## 12. Use Cases for Stream Processing

Common applications:

* Fraud detection
* Monitoring and alerting
* Real-time analytics
* Event-driven architectures

Stream processing enables timely responses to changing data.