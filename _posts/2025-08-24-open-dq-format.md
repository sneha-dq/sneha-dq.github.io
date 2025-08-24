---
title: "Do We Need an Open Format for Data Quality, Observability, and Governance?"
date: 2025-08-24
description: Just as Iceberg, Delta, and Hudi brought standardization to data lakes, the next frontier may be a true open standard for data quality, observability, and governance.
categories: [data-architecture, data-quality, data-governance, data-observability]
tags: [open-lineage, great-expectations, soda, openmetadata, data-quality, future-vision]
---

### From Open Table Formats to Open DQ Standards

In the last decade, the data world has seen a major shift. **HDFS and Hive** once dominated the big data ecosystem, but they lacked flexibility, transactional guarantees, and ease of use.  

This led to the rise of **open table formats** like **Apache Iceberg, Delta Lake, and Apache Hudi**, which brought schema evolution, ACID transactions, and a universal layer for data lakes.  

Now, the same question is being asked in a different domain:  
👉 *Can we do something similar for **data quality, observability, and governance**?*  

---

### The Current Fragmented Landscape

Unlike storage, the **DQ/observability/governance space** doesn’t yet have one clear open standard. Instead, we have:

- **Great Expectations (GX)** – “Expectations” as shareable quality checks.  
- **SodaCL** – A YAML-based open syntax for data quality rules.  
- **OpenLineage** – JSON-based events for job and dataset lineage.  
- **Marquez** – Reference implementation of OpenLineage.  
- **OpenMetadata** – Unified APIs and schemas for catalog, lineage, quality, and policies.  
- **WhyLogs / Evidently** – Open profiling and monitoring for ML/data drifts.  

Each is powerful, but **none is a universal standard** like Iceberg has become for data lakes.  

---

### What Would an “Iceberg for DQ” Look Like?

If we were to design an **open format for data quality/observability/governance**, it would likely need:

1. **A Standard DQ Rule Definition Language**  
   - Reusable, declarative, portable across systems.  
   - (Imagine SodaCL + GX merging into a single YAML/JSON spec.)  

2. **A Unified Metadata Schema**  
   - Covering datasets, lineage, policies, quality scores, owners.  
   - Compatible with tools like OpenMetadata.  

3. **Event-Driven Observability**  
   - Using an extension of **OpenLineage** to capture not just lineage, but also data quality results and governance events.  

4. **Polyglot Compatibility**  
   - Work seamlessly across RDBMS, NoSQL, open table formats, cloud warehouses, and streaming systems.  

5. **Interoperability with Governance**  
   - Ability to link rules with business glossaries, compliance policies, and data contracts.  

---

### Why Do We Need It?

- **Polyglot Data Architectures**: Enterprises use Postgres, MongoDB, Iceberg, Kafka, Snowflake — all at once. A single observability format would avoid tool sprawl.  
- **Data Contracts**: An open standard would enforce *machine-readable guarantees* across producers and consumers.  
- **Portability**: Avoid lock-in to one vendor’s observability tool.  
- **Trust**: Like Iceberg made data lakes reliable, an open DQ format could make *data health* reliable.  

---

### Signs of Progress

- **OpenLineage** is already being adopted widely, suggesting lineage might be the “first pillar” of this open format.  
- **SodaCL and GX** hint that communities are moving toward a **shared language for data checks**.  
- **OpenMetadata** could evolve into the metadata backbone for this ecosystem.  

It feels like the **building blocks are here**, but they are still scattered.  

---

### The Road Ahead

We might be heading toward a future where:  

- **OpenLineage++** = lineage + observability events.  
- **OpenDQ (hypothetical)** = YAML/JSON spec for quality and contracts.  
- **OpenMetadata** = governance schema + API.  

Together, these could form the **Iceberg-equivalent for DQ/Observability/Governance** — a universal open layer that every data platform could adopt.  

---

### Final Thought

Just as **HDFS → Hive → Iceberg** marked the progression in storage,  
we may soon see a similar evolution:  

**Great Expectations + SodaCL + OpenLineage + OpenMetadata → OpenDQ Standard.**  

The organizations that embrace such a standard early will likely build the **most trusted, interoperable, and future-proof data ecosystems**.  

---

✅ *What do you think? Should the data community push for a unified open standard for DQ/Observability, or will multiple specialized frameworks continue to coexist?*