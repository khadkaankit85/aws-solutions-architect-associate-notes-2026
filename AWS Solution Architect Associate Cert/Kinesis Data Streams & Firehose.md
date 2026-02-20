> [!abstract] What is it?
> **Amazon Kinesis** is a set of services for **real‑time data ingestion, processing, and delivery** at scale.  
> For the SAA exam, the two core services to understand are **Kinesis Data Streams** and **Kinesis Data Firehose**.

---

## Kinesis Data Streams

### Overview
Kinesis Data Streams is used for **real‑time streaming data** where you need **custom processing**, **low latency**, and **fine‑grained control**.

Typical producers include:
- Application logs
- Clickstreams
- IoT telemetry
- Game events

Consumers process data in near real time using:
- Custom applications
- AWS Lambda
- Kinesis Client Library (KCL)

---

### Core Concepts

#### Stream
A stream is a sequence of data records ordered by **partition key**.

#### Shards
- A shard is the basic unit of capacity
- Each shard supports:
  - 1 MB/sec write
  - 2 MB/sec read
- Scaling is done by **adding or removing shards**

#### Records
Each record contains:
- Data blob
- Partition key
- Sequence number

---

### Data Retention
- Default: **24 hours**
- Configurable up to **365 days**
- Enables replay and reprocessing

---

### Processing Model
- Consumers **pull** data from shards
- Multiple consumers can read the same stream independently
- Ordering is guaranteed **per partition key**

---

### When to Use Data Streams
- You need **real‑time processing**
- You need **custom logic**
- You need **data replay**
- You need **multiple consumers**

---

## Kinesis Data Firehose

### Overview
Kinesis Data Firehose is used for **near‑real‑time delivery** of streaming data to destinations **without managing consumers or scaling**.

Firehose is **fully managed** and **serverless**.

---

### Destinations
Firehose can deliver data to:
- Amazon S3
- Amazon Redshift
- Amazon OpenSearch
- Third‑party services (Splunk, Datadog)

---

### Processing Model
- Producers send data to Firehose
- Firehose buffers data
- Data is delivered in batches
- Optional Lambda transformation before delivery

---

### Key Characteristics
- No data retention
- No replay capability
- Automatic scaling
- Near‑real‑time (seconds to minutes)

---

### When to Use Firehose
- You want **simple ingestion**
- You don’t need custom consumers
- You don’t need replay
- You want data delivered to storage or analytics services

---

## Data Streams vs Firehose (SAA Focus)

| Feature | Data Streams | Firehose |
|---|---|---|
| Processing | Real‑time | Near‑real‑time |
| Consumers | Custom | Managed |
| Replay | Yes | No |
| Scaling | Manual | Automatic |
| Use Case | Streaming apps | Data delivery |

---

> [!tip] Exam Tip  
> If the question mentions **real‑time processing, replay, or multiple consumers**, choose **Data Streams**.  
> If it mentions **simple ingestion and delivery to S3/Redshift**, choose **Firehose**.

<span style="float:left">← [[SNS]]</span><span style="float:right">[[SQS vs SNS vs Kinesis]] →</span>
