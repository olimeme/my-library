## Chapter 4: Encoding and Evolution

## 1. Overview

Chapter 4 focuses on **how data is encoded for storage and transmission**, and how systems can **evolve schemas over time** without breaking compatibility. This is critical for long-lived, distributed systems where different components may run different versions simultaneously.

Key themes:

* Data encoding formats
* Backward and forward compatibility
* Schema evolution in practice

* Backward compatibility - newer code can read data that was written by older code.
* Forward compatibility - older code can read data that was written by newer code.

---

## 2. Formats for Encoding Data

Applications need to encode data for:

* Writing to disk
* Sending over the network
* Inter-process communication

An encoding format defines how in-memory objects are translated into bytes.

---

## 3. Language-Specific Encoding Formats

### 3.1 Native Serialization

Many programming languages provide built-in serialization mechanisms (e.g., Java Serialization, Python pickle).

#### Problems with Language-Specific Formats

* Tightly coupled to a specific programming language
* Poor forward and backward compatibility
* Security risks when deserializing untrusted data
* Hard to inspect or debug

These formats are rarely suitable for long-term storage or public APIs.

---

## 4. Text-Based Formats

### 4.1 JSON, XML, and CSV

Text-based formats are:

* Human-readable
* Widely supported
* Easy to debug

#### Advantages

* Language-agnostic
* Flexible schemas

#### Disadvantages

* Larger size (inefficient encoding)
* Slower parsing
* Ambiguity around data types (e.g., numbers, dates)

CSV is particularly limited due to lack of schema and type information.

---

## 5. Binary Encoding Formats

Binary formats aim to be:

* More compact
* Faster to parse
* Explicit about data types

---

### 5.1 Thrift and Protocol Buffers

Characteristics:

* Require a predefined schema
* Generate code for multiple languages
* Use numeric field tags

#### Benefits

* Efficient encoding
* Strong schema evolution support

#### Schema Evolution Rules

* Fields can be added or removed
* Field numbers must not be reused
* Unknown fields are ignored

---

### 5.2 Avro

Avro differs from Thrift and Protobuf:

* Schema is stored with the data (or alongside it)
* No field tags in encoded data
* Uses schema resolution at read time

#### Advantages

* Excellent for schema evolution
* Compact encoding
* Well-suited for big data systems

Used heavily in:

* Hadoop ecosystem
* Kafka-based pipelines

---

## 6. Modes of Dataflow

### 6.1 Dataflow Through Databases

When:

* Applications write encoded data to a database
* Future versions of the application read old data

Requirements:

* Backward compatibility
* Careful handling of missing or extra fields

---

### 6.2 Dataflow Through Services (REST and RPC)

Services communicate via APIs.

#### REST

* Uses HTTP and text-based formats (often JSON)
* Simple and widely adopted

#### RPC

* Resembles local function calls
* Often uses binary encodings

Challenges:

* Tight coupling between clients and servers
* Versioning APIs without breaking clients

---

### 6.3 Asynchronous Message Passing

* Communication via message brokers
* Decouples producers and consumers
* Improves resilience

Message formats must support:

* Schema evolution
* Backward and forward compatibility

---

## 7. Schema Evolution

Schema evolution is the ability to:

* Change data schemas over time
* Continue supporting old and new versions

### Compatibility Types

* **Backward compatibility**: new code reads old data
* **Forward compatibility**: old code reads new data

Binary formats with explicit schemas handle evolution best.

---

## 8. Versioning and Compatibility Strategies

Best practices:

* Never change the meaning of existing fields
* Use optional fields with defaults
* Avoid removing required fields
* Test compatibility between versions

Schema registries can help manage versions centrally.

---

## 9. Trade-offs in Encoding Choices

| Format Type       | Readability | Size   | Performance | Evolution Support |
| ----------------- | ----------- | ------ | ----------- | ----------------- |
| Language-specific | Low         | Medium | Fast        | Poor              |
| Text-based        | High        | Large  | Slow        | Moderate          |
| Binary            | Low         | Small  | Fast        | Strong            |

Choice depends on system requirements and constraints.

---

## 10. Summary of Chapter 4

Chapter 4 emphasizes that:

* Data encoding choices have long-term consequences
* Schema evolution is unavoidable in real systems
* Backward and forward compatibility are essential
* Binary formats with schemas provide the strongest guarantees

Careful encoding design enables systems to evolve safely over time.
