### 🧩 Snowflake Success Plan

This document outlines the mutual success plan for the Duel Tech evaluation of the Snowflake Data Cloud, based on our joint discovery and the accompanying `duel_tech_quickstart.md` technical guide.

#### 1. 🚨 Business Challenges
* **Data pipelines are unscalable and brittle**, relying on full daily snapshots from MongoDB that cannot support growth beyond 25K advocates.
* **Excessive engineering effort** (est. 160 hours/month) is spent on manual Change Data Capture (CDC) and pipeline maintenance.
* **Analytics is bottlenecked**, with insights limited to 3 SQL users, blocking the marketing team from self-service and creating 72-hour reporting delays.

#### 2. 🎯 Business Objectives
* **Build a scalable data foundation** that supports linear scaling to 100K+ advocates.
* **Automate data transformation** and CDC to reduce engineering overhead and improve data freshness from 72 hours to <10 minutes.
* **Enable self-service analytics** for the marketing team (15+ users) via their existing BI tool, Quicksight.


#### 3. 🧠 Use Cases
* **Phase 1 (POC): Foundational GAV Data Model:** Ingest advocate data (advocates, tasks, posts, companies) from daily MongoDB exports into a structured, reliable data model.
* **Phase 1 (POC): Automated CDC & Transformation:** Build an automated, incremental pipeline to calculate the core "Gross Advocacy Value" (GAV) business metric using dbt.
* **Phase 1 (POC): BI & Governance:** Deliver the trusted GAV model to Quicksight in Direct Query mode and automatically secure all PII data.
* **Phase 2 (Future): Advanced Analytics:** Enable real-time streaming, natural language queries (Cortex), and self-service applications (Streamlit).

#### 4. ✅ Success Criteria

| Objective | Success Criteria | Snowflake Feature(s) | Suggested Activity |
|:---|:---|:---|:---|
| **Build a scalable data foundation** | Validate a scalable ingestion pattern (micro-batch or streaming) that is more efficient and reliable than daily full snapshots. | **Snowpipe**, **Snowpipe Streaming**, **Partner Connect** (e.g., Fivetran), **External Access** | Implement **Module 2 (Snowpipe)** as the immediate improvement and benchmark against one 3rd-party connector to evaluate long-term TCO. |
| **Automate data transformation** & reduce engineering overhead | Automate the manual CDC process, reducing data latency from 72 hours to <10 minutes. | **Dynamic Tables** | Complete **Module 3 (Dynamic Tables)** from the Quickstart to build an automated bronze-to-silver pipeline. |
| **Build a scalable & governed data foundation** | 1. Implement the "Gross Advocacy Value" (GAV) model in a version-controlled, production-ready way. <br> 2. Secure all advocate PII (e.g., email) from non-privileged users. | **Native dbt Integration**, **Dynamic Data Masking** | 1. Complete **Module 3 (dbt)** to build the GAV metric models. <br> 2. Complete **Module 6 (Security)** to apply a masking policy to the advocate email column. |
| **Enable self-service analytics** | Successfully deliver the GAV model to Quicksight, eliminating the need for SPICE and solving the 72-hour reporting delay. | **Quicksight Connector (Direct Query)**, **Warehouse Caching** | Complete **Module 4 (QuickSight)**, connecting a dashboard in **Direct Query mode** to the new Gold GAV views. |
| **Reduce TCO by up to 75%** | Validate a new cost model by separating ingestion, transformation, and analytics workloads. | **Workload Isolation (Warehouses)**, **Resource Monitors** | 1. Use the **Module 1 (Terraform)** scripts to deploy separate `INGESTION`, `TRANSFORMATION`, and `ANALYTICS` warehouses. <br> 2. Complete **Module 5 (Cost Optimization)** to apply resource monitors. |

#### 5. 💡 Notes & Recommendations
* **Terraform First:** The technical team strongly prefers an "infrastructure as code" workflow. The evaluation should prioritize **Module 1: Option A (Deploy with Terraform)** for all resource creation. This will build confidence and align with existing practices.
* **Focus on the Foundation:** This evaluation is focused on **Phase 1: Build the GAV Foundation**. Success is defined by proving the core pipeline (Ingestion -> Dynamic Tables -> dbt -> Quicksight). Features like Cortex Analyst and Snowpipe Streaming are high-value "fast follows" for Phase 2.

- [Terraforming Snowflake](https://quickstarts.snowflake.com/guide/terraforming_snowflake/index.html#0)
- [dbt on Snowflake Guide](https://docs.snowflake.com/en/user-guide/data-engineering/dbt-projects-on-snowflake)
