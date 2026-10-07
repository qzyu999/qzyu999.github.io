---
layout: default
name: Lighthouse - GenAI Data Lake Exploration Platform
date: 2025-10-20
context: Data Engineering & Lakehouse Lineage
toc: true
toc_sticky: true
toc_label: "Table of Contents"
toc_icon: "cog"
excerpt_separator: A pluggable AI data lake discovery platform combining an embedded DuckDB SQL analytics engine, interactive column-level React Flow data lineage, and automated AI data wiki documentation synced via GitHub Pull Requests.
---

# Lighthouse: GenAI Data Lake Exploration Platform

Navigating enterprise data lakes—spanning thousands of Parquet files, Iceberg tables, and dbt models—often involves disjointed tools: slow cloud query engines, static and outdated wiki documentation, and opaque data lineage. Analysts and engineers frequently struggle to trace how specific business metrics are derived, or what downstream reports will break if a column definition changes.

**Lighthouse** is an open-source, pluggable AI data lake discovery and exploration platform. It unifies an embedded **DuckDB OLAP analytics engine**, an **interactive column-level lineage graph**, and an **AI-powered data wiki** that writes back schema documentation through automated GitHub Pull Requests.

[GitHub Repository: Lighthouse](https://github.com/qzyu999/Lighthouse)

---

# Architecture Overview

```
                          +-----------------------------------+
                          |      DATA LAKE STORAGE TIER       |
                          |   Parquet / Apache Iceberg / S3   |
                          +-----------------+-----------------+
                                            |
                                            v
+-----------------------------------------------------------------------------------+
|                               LIGHTHOUSE PLATFORM                                 |
|                                                                                   |
|  +---------------------------+   +----------------------+   +------------------+  |
|  | Embedded DuckDB Engine    |   | Column Lineage DAG   |   | AI Data Wiki     |  |
|  | Sub-second SQL analytics  |   | React Flow parser    |   | Multi-persona doc|  |
|  | TPC-H query benchmarks    |   | Impact analysis      |   | generation       |  |
|  +---------------------------+   +----------------------+   +------------------+  |
+-------------------------------------------+---------------------------------------+
                                            |
                                            v
                          +-----------------------------------+
                          |    GIT-AS-CATALOG GOVERNANCE      |
                          |   Automated GitHub Pull Requests  |
                          |      (Metadata as Code / CI)      |
                          +-----------------------------------+
```

---

# Key Features

### 1. Embedded DuckDB OLAP Query Engine
Lighthouse eliminates the latency and cloud cost of spinning up Spark or Trino clusters for ad-hoc dataset inspection:
* **Zero-Setup Analytics:** Queries Parquet files and Iceberg tables directly from cloud object stores (S3, GCS) or local disks using DuckDB's vectorized C++ query execution engine.
* **TPC-H Benchmark Performance:** Handles multi-gigabyte analytical joins and window aggregations with sub-second response times on standard developer workstations.
* **Schema Inference:** Instantly detects nested types, variant JSON columns, and partition layouts without requiring catalog pre-registration.

### 2. Interactive Column-Level Lineage (React Flow)
Traditional table-level lineage graphs fail to answer critical engineering questions such as *"Where does `adjusted_revenue` originate, and which downstream dashboards consume it?"*
* **SQL AST Parsing:** Automatically analyzes SQL transformations, view definitions, and dbt models to trace column derivations through intermediate joins, aggregations, and window functions.
* **Interactive DAG Visualization:** Built with React Flow, providing full pan/zoom, interactive node highlighting, and backward/forward dependency tracing.
* **Impact Analysis:** Allows engineers to simulate column renaming or deprecation, instantly highlighting all downstream breaking changes before production deployment.

```sql
-- Automated lineage extraction traces column provenance through complex SQL:
WITH regional_sales AS (
    SELECT 
        customer_id,
        SUM(order_amount * (1 - discount_rate)) AS net_revenue
    FROM raw_orders
    GROUP BY customer_id
)
SELECT 
    c.country_code,
    AVG(r.net_revenue) AS avg_country_spend
FROM regional_sales r
JOIN raw_customers c ON r.customer_id = c.id
GROUP BY c.country_code;
```

### 3. AI-Powered Data Wiki & Multi-Persona Documentation
Maintaining data documentation is notoriously difficult to enforce across engineering teams:
* **Automated Cataloging:** LLM agents inspect column data types, statistical distributions (min, max, null count, distinct values), and sample records to draft comprehensive documentation for schemas and metric definitions.
* **Multi-Persona Prompting:** Tailors documentation tone and depth for different audiences—technical documentation for data engineers, compliance annotations for data governance, and business glossary definitions for product analysts.

### 4. Git-as-Catalog Governance
Unlike SaaS data catalogs that store documentation in proprietary silos, Lighthouse treats documentation as version-controlled code:
* **Automated GitHub PR Sync:** When an engineer approves or updates AI-generated table documentation, Lighthouse commits the changes directly to the repository and opens a structured GitHub Pull Request (`gh pr create`).
* **CI/CD Integration:** Integrates into standard code review workflows, ensuring documentation is versioned, peer-reviewed, and deployed alongside data pipeline code.

---

# Tech Stack

* **Frontend:** TypeScript, React, React Flow, Tailwind CSS.
* **Query Engine:** DuckDB, Apache Arrow, Python.
* **Backend API:** FastAPI, Pydantic, FastMCP.
* **Governance & CI:** GitHub API, Git CLI.
