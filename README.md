### 🧩 Snowflake Success Plan

This document outlines the mutual success plan for Duel Tech’s growth on the Snowflake Data Cloud, based on our joint discovery and the accompanying [POV Quickstart](duel_tech_quickstart.md) technical guide.

#### 1. 🚨 Business Challenges
* **Data pipelines are unscalable and brittle**, relying on full daily snapshots from MongoDB that cannot support growth beyond 25K advocates.
* **Data pipelines lack robustness** and are not as healthy as desired, creating risk for future scaling.
* **Analytics is bottlenecked** by a small technical team, blocking non-technical users from self-service and creating **24-hour** reporting delays.

#### 2. 🎯 Business Objectives
* **Build a scalable data foundation** that supports linear scaling to 100K+ advocates.
* **Automate data transformation** and CDC to improve pipeline robustness and **establish the capability** for future low-latency use cases (improving from the current 24-hour freshness).
* **Enable self-service analytics** for all users (approx. 60+) via their existing BI tool, Quicksight.


#### 3. 🧠 Use Cases
* **Phase 1 (POC): Foundational GAV Data Model:** Ingest advocate data (advocates, tasks, posts, companies) from daily MongoDB exports into a structured, reliable data model.
* **Phase 1 (POC): Automated CDC & Transformation:** Build an automated, incremental pipeline to calculate the core "Gross Advocacy Value" (GAV) business metric using dbt.
* **Phase 1 (POC): BI & Governance:** Deliver the trusted GAV model to Quicksight (validating against the current SPICE architecture) and automatically secure all PII data.
* **Phase 2 (Future): Advanced Analytics:** Enable real-time streaming, natural language queries (Cortex), and self-service applications (Streamlit).

#### 4. ✅ Success Criteria

| Objective | Success Criteria | Snowflake Feature(s) | Suggested Activity |
|:---|:---|:---|:---|
| **Build a scalable data foundation** | Validate a scalable ingestion pattern (micro-batch or streaming) that is more efficient and reliable than daily full snapshots. | **Snowpipe**, **Snowpipe Streaming**, **Partner Connect** (e.g., Fivetran), **External Access** | Implement **Module 2 (Snowpipe)** as the immediate improvement and benchmark against one 3rd-party connector to evaluate long-term TCO. |
| **Build a scalable & governed data foundation** | 1. Implement the "Gross Advocacy Value" (GAV) model in a version-controlled, production-ready way. <br> 2. Secure all advocate PII (e.g., email) from non-privileged users. | **Native dbt Integration**, **Dynamic Data Masking** | 1. Complete **Module 3 (dbt)** to build the GAV metric models. <br> 2. Complete **Module 6 (Security)** to apply a masking policy to the advocate email column. |
| **Enable self-service analytics** | Successfully deliver the GAV model to Quicksight and validate performance against the current 24-hour SPICE reporting model. | **Quicksight Connector (Direct Query)**, **Warehouse Caching** | Complete **Module 4 (QuickSight)**, connecting a dashboard and benchmarking against the existing Gold GAV views. |
| **Validate efficient cost model** | Validate a more efficient cost model by separating ingestion, transformation, and analytics workloads. | **Workload Isolation (Warehouses)**, **Resource Monitors** | 1. Use the **Module 1 (Terraform)** scripts to deploy separate `INGESTION`, `TRANSFORMATION`, `ANALYTICS` warehouses. <br> 2. Complete **Module 5 (Cost Optimization)** to apply resource monitors. |

#### 5. 💡 Notes & Recommendations
* **Terraform First:** The technical team strongly prefers an "infrastructure as code" workflow. The evaluation should prioritize **Module 1: Option A (Deploy with Terraform)** for all resource creation. This will build confidence and align with existing practices.
* **Focus on the Foundation:** This evaluation is focused on **Phase 1: Build the GAV Foundation**. Success is defined by proving the core pipeline (Ingestion -> Dynamic Tables -> dbt -> Quicksight). Features like Cortex Analyst and Snowpipe Streaming are high-value "fast follows" for Phase 2.

- [Terraforming Snowflake](https://quickstarts.snowflake.com/guide/terraforming_snowflake/index.html#0)
- [dbt on Snowflake Guide](https://docs.snowflake.com/en/user-guide/data-engineering/dbt-projects-on-snowflake)
- [Using a Git repository in Snowflake](https://docs.snowflake.com/en/developer-guide/git/git-overview)
