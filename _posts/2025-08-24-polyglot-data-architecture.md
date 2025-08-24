---
title: "7 Database Architectures: From RDBMS to Open Table Formats"
date: 2025-08-24
description: A deep dive into modern database architectures, from relational systems to open table formats, and how to choose the right one.
categories: [data-architecture]
tags: [rdbms, nosql, hdfs, open-table-format, data-lakehouse, graph-db, columnar-db, polyglot]
---

Data storage and processing have evolved massively in the last two decades. From **traditional relational databases (RDBMS)** to **modern open table formats**, the ecosystem offers multiple architectural options. Choosing the right one depends on **data type, access patterns, scalability needs, and ecosystem fit**.  

In this blog, we’ll break down **7 major database/storage architectures**, how they differ, their progression, and when to use each — along with a note on **polyglot persistence**, where multiple options coexist in the same ecosystem.

---

## 1. Relational Databases (RDBMS)
**Examples:** PostgreSQL, MySQL, SQL Server, Oracle  

- **Characteristics:**  
  - Structured, schema-based tables.  
  - Strong **ACID guarantees**.  
  - Best for **OLTP workloads** (transactions, financial systems, ERP).  
- **When to use:** Critical when you need **consistency, structured schemas, joins**, and transactional integrity.  
- **Limitations:** Hard to scale horizontally, not optimized for semi/unstructured data.  

---

## 2. NoSQL Databases
**Examples:** MongoDB, Cassandra, DynamoDB, MarkLogic, CosmosDB  

- **Characteristics:**  
  - Schema-flexible, handles **JSON, XML, key-value, wide-column, or graph data**.  
  - Optimized for **horizontal scale and high availability**.  
  - Each type is tuned for specific workloads (document stores, key-value, graph, etc.).  
- **When to use:** Applications needing **flexibility, scale, and low-latency lookups** (social apps, IoT, catalogs, real-time feeds).  
- **Progression:** Emerged to complement RDBMS for web-scale apps.  

---

## 3. Distributed File Systems (HDFS)
**Examples:** HDFS (Hadoop Distributed File System)  

- **Characteristics:**  
  - File-based, not a database.  
  - Stores raw files (CSV, Parquet, images, logs).  
  - Needs engines like **Hive, Spark, or Presto** for querying.  
- **When to use:** Storing **large volumes of raw data** with durability and replication.  
- **Limitations:** Lack of schema evolution, governance, and transactional consistency.  

---

## 4. Open Table Formats
**Examples:** Apache Iceberg, Apache Hudi, Delta Lake  

- **Characteristics:**  
  - Built on top of object stores (S3, ADLS, GCS).  
  - Support **schema evolution, ACID transactions, time travel, and governance**.  
  - Decoupled from compute → works with Spark, Flink, Presto, Trino, etc.  
- **When to use:** For **data lakes turning into lakehouses**, where you need both OLTP-like guarantees and OLAP queries.  
- **Progression:** Evolution from HDFS + Hive to modern **Lakehouse architectures**.  

---

## 5. Columnar Databases
**Examples:** ClickHouse, Vertica, Amazon Redshift  

- **Characteristics:**  
  - Stores data in **columns** instead of rows → efficient for aggregation and analytics.  
  - Extremely fast **OLAP queries**.  
- **When to use:** Analytical workloads, dashboards, BI systems.  
- **Limitations:** Not good for OLTP or high-write transaction systems.  

---

## 6. Graph Databases
**Examples:** Neo4j, Amazon Neptune, TigerGraph  

- **Characteristics:**  
  - Store entities (nodes) and relationships (edges).  
  - Optimized for **graph traversal queries** (shortest path, recommendations).  
- **When to use:** Fraud detection, social networks, knowledge graphs, recommendation engines.  

---

## 7. Search/Indexing Databases
**Examples:** Elasticsearch, OpenSearch, Solr  

- **Characteristics:**  
  - Designed for **full-text search, fuzzy matching, and indexing**.  
  - Often used alongside other databases to improve search experiences.  
- **When to use:** Search-heavy applications, log analytics, observability stacks.  

---

## The Evolution: HDFS → Open Table Formats
- **HDFS era:** Store everything cheaply but query engines were disconnected and governance was weak.  
- **Open Table Formats era:** Added **ACID, schema evolution, and time travel** to raw file storage.  
- **Result:** Data lakes evolved into **data lakehouses**, blurring the line between OLTP-like operations and OLAP analytics.  

---

## Polyglot Persistence: The Reality
No single database fits all needs. Modern organizations adopt **polyglot persistence** — using different databases for different workloads:  
- **RDBMS** for core transactions  
- **NoSQL** for flexible, high-scale apps  
- **Open Table Formats** for lakehouse analytics  
- **Graph DB** for relationships  
- **Search DB** for discovery  

This mix ensures **best-of-breed performance** depending on the workload.  

---

## How to Decide Which One to Use?
- **Workload type:** OLTP (transactions) → RDBMS/NoSQL; OLAP (analytics) → Columnar/Open Table Formats  
- **Data type:** Structured → RDBMS; Semi/unstructured → NoSQL/Open Table Formats; Graph → Graph DB  
- **Scalability:** Need horizontal scaling? → NoSQL, Open Table Formats, Columnar DB  
- **Governance & Transactions:** Strong consistency → RDBMS, Delta Lake, Hudi, Iceberg  

---

## Final Thoughts
The progression from **RDBMS → HDFS → Open Table Formats** shows how the industry moved from **rigid, schema-first systems** to **flexible, scalable, and governed architectures**.  

But it’s not about *replacing* one with another — it’s about **choosing the right tool for the right job** and often using multiple in harmony under a **polyglot architecture**.

---