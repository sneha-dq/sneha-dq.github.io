---
title: "Designs Can Deceive, But Data Won’t: A Real-World Lesson in Migration Pitfalls"
date: 2025-07-29
description: A real-world story of how a data migration looked perfect in design but unraveled under real data load, proving that data never lies.
categories: [data-engineering]
tags: [data-engineering, data-migration, real-world-lessons, data-driven-design, data-tech-debt]
---

> *“All models are wrong, but some are useful.” — George Box*  
In data systems, sometimes all designs seem right — until the data speaks.

Recently, while working on a data modernization project for an investment firm, we learned this the hard way. We were moving from **MarkLogic**, a multi-model database, to **Databricks**, aiming to unify data analytics, simplify pipelines, and embrace scalable architecture. Everything looked good on paper. The architecture diagrams were clean. The workflows were refactored. But then came the data. And it didn’t lie.

---

## 🚨 The Showstopper

As part of the migration, we had to replicate a key workflow originally running in MarkLogic. The workflow involved pulling enriched investment data via APIs, transforming it, and funneling it into analytics layers.

The new Databricks-based design seemed robust. But once live data started flowing in, we were hit with a crisis:

- **API calls shot up 10x compared to the MarkLogic version.**  
- **Millions of records/day** started triggering unexpected volumes of requests.  
- **The downstream API servers nearly collapsed.**  
- The system began **timing out, throttling, and failing silently** in some cases.

We went from “Everything looks perfect” to “Why is the system choking?” in hours.

---

## 🕵️ What Went Wrong?

The design was functionally correct — but **functionality ≠ efficiency**.

- In MarkLogic, **batching** and **smart querying** were used natively.  
- In Databricks, the new design **looped over smaller chunks**, triggering API calls per row instead of per batch.  
- The shift in **processing paradigm** (document-oriented to distributed compute) wasn’t fully accounted for during replication.

On paper, the two workflows *looked* identical. But in execution, they couldn’t have been more different. And it was the **data behavior** — not the diagrams — that revealed the flaw.

---

## 📊 The Unfiltered Truth: Data > Design

Designs can be deceiving. They can be overly abstract, too generic, or misrepresent real-world execution. But **data always brings out the truth** — in usage patterns, performance metrics, system bottlenecks, and more.

In this case:
- Data exposed **scaling flaws**.
- It highlighted **design blind spots**.
- It forced us to **rethink how workloads were parallelized and optimized**.

---

## ✅ Key Learnings

1. **Always Validate Design with Volume Simulation**  
   Don’t wait for production load to reveal flaws. Use synthetic data at scale to validate assumptions.

2. **Understand the Source System’s Strengths**  
   MarkLogic handled things differently for a reason. Don’t assume a 1:1 mapping will retain performance.

3. **Watch Out for Hidden Multipliers**  
   Looping through APIs? Transformations per record? These scale silently but explode under load.

4. **Monitor Early, Monitor Often**  
   Set up detailed telemetry around API usage, latency, error rates — even before full rollout.

5. **Data > Diagrams**  
   Designs may show intent, but only data can show reality.

---

## 💡 Good Practices for Migration Projects

- **Build POCs with real data slices** to see system behavior.
- **Involve performance benchmarking** as a core part of migration—not as an afterthought.
- **Log everything at scale.** Logging 100 rows vs 10 million rows is a different challenge.
- **Design for worst-case data scenarios**, not just best-case flow.

---

## 🔁 Final Thoughts

Modern data systems are incredibly powerful — but also unforgiving when design choices go unchecked. We often trust our designs because they "make sense". But **data doesn't care what makes sense** — it only reflects what *actually happens*.

In our case, the wake-up call came just in time. We fixed the API logic, introduced bulk-fetching patterns, and implemented request throttling and retries. But the larger lesson remains:

> **Trust your data more than your design. Let it be your loudest critic.**
