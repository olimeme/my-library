## Chapter 2: Data Models and Query Languages

## 1. Introduction to Data Models

A **data model** defines how data is structured, stored, and manipulated. It shapes:

* How applications are written
* How data is queried and updated
* How systems evolve over time

Choosing the right data model is one of the most important architectural decisions in a data-intensive application.

---

## 2. Relational Model

### 2.1 Overview

The **relational model**, introduced by Edgar F. Codd in 1970, represents data as:

* **Relations (tables)**
* **Rows (tuples)**
* **Columns (attributes)**

Each table has a defined schema, and relationships are expressed using **foreign keys**.

### 2.2 Strengths of the Relational Model

* Strong theoretical foundation
* Declarative query language (**SQL**)
* Powerful joins across tables
* Data integrity via constraints
* Mature tooling and ecosystem

Relational databases are particularly good for applications with:

* Well-understood schemas
* Complex queries
* Strong consistency requirements

### 2.3 Schema-on-Write

Relational databases typically enforce **schema-on-write**:

* Data must conform to the schema before being written
* Errors are caught early
* Schema changes can be costly

---

## 3. NoSQL Data Models

NoSQL systems emerged to address scalability, flexibility, and performance limitations of traditional relational databases.

### 3.1 Key-Value Stores

* Store data as a simple key → value mapping
* Very fast reads and writes
* Limited querying capabilities

**Use cases**:

* Caching
* Session storage
* User preferences

---

### 3.2 Document Model

* Data stored as **documents** (e.g., JSON, BSON)
* Documents contain nested structures
* Schema is flexible or implicit

#### Advantages

* Natural fit for hierarchical data
* Reduces need for joins
* Easier schema evolution

#### Disadvantages

* Harder to enforce data consistency
* Poor support for cross-document relationships

Document databases typically use **schema-on-read**.

---

### 3.3 Column-Family (Wide-Column) Stores

* Data stored by columns rather than rows
* Inspired by Google Bigtable
* Optimized for large-scale, distributed workloads

**Use cases**:

* Time-series data
* Analytical queries
* Large datasets with predictable access patterns

---

### 3.4 Graph Data Model

Graph databases represent data as:

* **Vertices (nodes)**
* **Edges (relationships)**

Edges can have properties and types.

#### When Graphs Are Useful

* Highly interconnected data
* Many-to-many relationships
* Traversal-heavy queries

**Examples**:

* Social networks
* Recommendation systems
* Fraud detection

---

## 4. Query Languages

### 4.1 Declarative vs Imperative Queries

* **Imperative**: specify how to compute results (step-by-step)
* **Declarative**: specify what result you want

Declarative queries allow the database to:

* Optimize execution
* Choose efficient query plans
* Improve performance without changing application code

SQL is a declarative language.

---

### 4.2 SQL

Key features:

* Joins
* Aggregations
* Subqueries
* Index utilization

SQL works well across different storage engines due to its abstraction over physical data layout.

---

### 4.3 Query Languages for NoSQL

Examples include:

* MongoDB query language
* Cassandra CQL
* Elasticsearch DSL

Many NoSQL query languages are **restricted** compared to SQL, trading expressiveness for performance and scalability.

---

### 4.4 Graph Query Languages

* **Cypher** (Neo4j)
* **SPARQL** (RDF)

Designed for expressing graph traversals concisely and efficiently.

---

## 5. Schema Flexibility and Evolution

### 5.1 Schema-on-Read vs Schema-on-Write

| Aspect          | Schema-on-Write | Schema-on-Read |
| --------------- | --------------- | -------------- |
| Validation      | At write time   | At read time   |
| Flexibility     | Low             | High           |
| Error detection | Early           | Late           |

Neither approach is inherently better; the choice depends on application needs.

---

## 6. Data Locality and Performance

* Document models encourage **data locality** by storing related data together
* Relational models normalize data, sometimes requiring joins
* Locality can significantly impact performance in distributed systems

---

## 7. Polyglot Persistence

**Polyglot persistence** means using multiple data storage technologies within one application, each chosen for a specific purpose.

Example:

* Relational DB for transactions
* Document DB for user profiles
* Search index for full-text search

This approach increases flexibility but adds operational complexity.
