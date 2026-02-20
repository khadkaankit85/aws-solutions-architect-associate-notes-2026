> [!abstract] What is it?
> **Data & Analytics on AWS** provides managed services to ingest, store, process, analyze, and visualize data at scale—ranging from ad‑hoc SQL queries to real‑time streaming pipelines and petabyte‑scale analytics.

---

## Amazon Athena
**Serverless, interactive SQL** over data in S3.

**Key concepts**
- Query data **in place** (no loading) using standard SQL
- Schema-on-read via **AWS Glue Data Catalog**
- Pay per data scanned → partitioning and columnar formats matter

**Best practices**
- Use **Parquet/ORC** + compression
- Partition by date/region to reduce scan size
- Ideal for ad‑hoc analysis, logs, and data lakes

---

## Amazon Redshift
**Managed data warehouse** for large-scale analytics.

**Key concepts**
- Columnar storage, MPP architecture
- **Leader node** (query planning) + **compute nodes**
- Optimized for complex joins and aggregations

**Deployment options**
- **Provisioned clusters** (predictable workloads)
- **Redshift Serverless** (auto-scaling, pay-per-use)

**Use cases**
- BI reporting
- Enterprise analytics
- Large historical datasets

---

## Amazon OpenSearch Service (Elasticsearch)
**Search and analytics engine** for near real-time insights.

**Key concepts**
- Index-based storage
- Full-text search, aggregations, dashboards
- Near real-time ingestion

**Use cases**
- Log analytics
- Application search
- Observability (metrics, traces)

**Note**
- Not a relational database
- Optimized for search, not joins

---

## Amazon EMR
**Managed big data processing** using open-source frameworks.

**Supported engines**
- Apache Spark
- Hadoop
- Hive
- Presto

**Key concepts**
- Runs on EC2 (or EKS)
- You manage cluster lifecycle
- High flexibility, more operational overhead

**Use cases**
- Large-scale batch processing
- Custom big data pipelines
- Legacy Hadoop workloads

---

## Amazon QuickSight
**Serverless BI and visualization** service.

**Key concepts**
- Connects to Athena, Redshift, S3, RDS
- SPICE in-memory engine for fast dashboards
- Pay-per-session or user-based pricing

**Use cases**
- Dashboards
- Business reporting
- Embedded analytics

---

## AWS Glue
**Serverless ETL and data catalog** service.

**Key components**
- **Glue Data Catalog**: central metadata store
- **Glue Jobs**: ETL using Spark
- **Glue Crawlers**: infer schemas automatically

**Use cases**
- Data lake ETL
- Schema discovery
- Preparing data for Athena/Redshift

---

## AWS Lake Formation
**Governance layer for data lakes**.

**Key concepts**
- Centralized permissions for S3 data
- Fine-grained access (table/column/row)
- Integrates with Glue, Athena, Redshift

**Use cases**
- Secure multi-team data lakes
- Compliance and access control

---

## Apache Flink (via Amazon Managed Service for Apache Flink)
**Stateful stream processing**.

**Key concepts**
- Event-time processing
- Exactly-once semantics
- Low-latency streaming analytics

**Use cases**
- Real-time fraud detection
- Streaming aggregations
- Stateful event processing

---

## Apache Kafka (Amazon MSK)
**Managed Kafka for streaming ingestion**.

**Key concepts**
- Topics, partitions, offsets
- High-throughput, durable streams
- Multiple consumers per topic

**Use cases**
- Event streaming backbone
- Log ingestion
- Real-time pipelines

---

## Big Data Ingestion Pipeline (Typical)
1. **Producers** → Kafka / Kinesis
2. **Stream processing** → Flink / Lambda
3. **Storage** → S3 data lake
4. **Catalog** → Glue
5. **Query** → Athena / Redshift
6. **Visualization** → QuickSight

---

## Service Selection (SAA Focus)

| Need | Service |
|---|---|
| Ad‑hoc SQL on S3 | Athena |
| Enterprise analytics | Redshift |
| Search/log analytics | OpenSearch |
| Big data processing | EMR |
| BI dashboards | QuickSight |
| ETL & metadata | Glue |
| Data lake governance | Lake Formation |
| Real-time streaming | Kafka / Flink |

---

> [!tip] Exam Tip  
> If the question mentions **S3 + SQL**, think **Athena**.  
> If it mentions **data warehouse**, think **Redshift**.  
> If it mentions **logs/search**, think **OpenSearch**.  
> If it mentions **ETL/catalog**, think **Glue + Lake Formation**.

<span style="float:left">← [[Serverless Overview — SAA]]</span><span style="float:right">[[Machine Learning]] →</span>
