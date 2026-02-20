> [!abstract] What is it? **Amazon Aurora** is a cloud‑optimized relational database built by AWS, compatible with **MySQL and PostgreSQL**, designed for high performance, availability, and scalability.

---

## High‑Level Overview

Aurora is not a traditional database engine. It is **AWS‑native**, meaning the storage and compute layers are decoupled and optimized for the cloud. MySQL and PostgreSQL compatibility means existing applications can connect using the same drivers and SQL syntax with minimal changes.

Aurora delivers up to **5× MySQL** and **3× PostgreSQL** performance compared to standard RDS engines.

---

## Storage Architecture

Aurora storage:

- Grows automatically in **10 GB increments**
- Scales up to **256 TB**
- Is shared across the cluster

Data is:

- Replicated **6 times**
- Across **3 Availability Zones**
- **4 copies required** for writes, **3 copies** for reads

Storage is **self‑healing** and striped across hundreds of volumes.

---

## High Availability and Scaling

Aurora uses a **cluster architecture**:

- **1 writer instance** (writes only)
- Up to **15 read replicas**

Failover is **instance‑level** and typically completes in **under 30 seconds**.

Aurora is **Multi‑AZ by design**, unlike RDS where Multi‑AZ is optional.

---

## Endpoints and Traffic Flow

Aurora provides multiple endpoints:

- **Writer endpoint**: always points to the current primary
- **Reader endpoint**: load balances across read replicas
- **Custom endpoints**: route traffic to specific subsets of replicas

Applications connect using endpoints, not instance IPs. During failover, endpoints automatically update with no application changes.

---

## Read Scaling

Read replicas:

- Scale reads horizontally
- Can be placed across AZs
- Support **auto scaling** based on load

Custom endpoints allow separating workloads, such as routing analytics queries to larger replicas.

---

## Cost

Aurora costs **more than standard RDS** but provides:

- Higher performance
- Built‑in HA
- Faster failover
- Better read scaling

---

## Aurora Serverless

Aurora Serverless automatically scales capacity up and down.

- No capacity planning
- Pay per second
- Ideal for unpredictable or intermittent workloads

---

## Global Aurora

Aurora Global Database:

- One primary read‑write region
- Up to **16 read‑only regions**
- Cross‑region replication under **1 second**
- Designed for low‑latency global reads and disaster recovery

---

## Advanced Features

### Backtrack

Restore data to a previous point in time **without restoring from backup**.

### Aurora Machine Learning

Run ML predictions directly from SQL using AWS ML services. Use cases include fraud detection and ad targeting.

### Babelfish for Aurora

Allows Aurora PostgreSQL to understand **T‑SQL**. Enables migration from SQL Server with minimal code changes using AWS SCT and DMS.

---

<br><br>

<span style="float:left">← [[Amazon RDS]]</span><span style="float:right">[[RDS Advanced]] →</span>