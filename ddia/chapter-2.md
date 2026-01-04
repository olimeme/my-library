## Chapter 2 — Data Models and Query Languages

### Why Data Models Matter

Data models:

* Shape how data is structured
* Influence how applications are written
* Affect performance and scalability

They are the **interface** between data and code.

---

### Relational Model

**Key characteristics**:

* Data stored in tables (rows & columns)
* Fixed schema
* SQL as query language

**Strengths**:

* Mature ecosystem
* Strong consistency guarantees
* Powerful joins

**Use cases**:

* Transactions
* Structured data
* Complex queries

---

### NoSQL Models

Motivations:

* Scalability
* Flexibility
* High availability

#### 1. Key-Value Stores

* Simple lookup by key
* Very fast
* Limited querying

Examples: Redis, DynamoDB

---

#### 2. Document Model

* Semi-structured (JSON-like)
* Schema-on-read
* Nested data

**Pros**:

* Flexible schema
* Natural mapping to application objects

**Cons**:

* Poor support for joins
* Data duplication

Examples: MongoDB, CouchDB

---

#### 3. Column-Family Stores

* Data grouped by columns
* Optimized for large-scale analytics

Examples: Cassandra, HBase

---

### Relational vs Document Model

| Aspect        | Relational     | Document           |
| ------------- | -------------- | ------------------ |
| Schema        | Fixed          | Flexible           |
| Joins         | Strong support | Weak/none          |
| Data locality | Poor           | Good               |
| Normalization | Encouraged     | Often denormalized |

---

### Query Languages

#### Declarative (e.g., SQL)

* Specify *what* you want
* Database decides *how*
* Easier to optimize

#### Imperative

* Specify step-by-step logic
* More control, less optimization

Declarative queries are generally preferred.

---

### Graph Data Models

Used when relationships are first-class citizens.

**Components**:

* Vertices (nodes)
* Edges (relationships)

**Use cases**:

* Social networks
* Recommendation systems
* Fraud detection

**Query languages**:

* Cypher
* SPARQL
* Gremlin

---

### Summary

* Different data models suit different problems
* Relational and NoSQL models are complementary
* Choose based on access patterns and relationships

---

### Key Takeaways

* System qualities matter as much as features
* Data models strongly influence system design
* There is no single best database

---
