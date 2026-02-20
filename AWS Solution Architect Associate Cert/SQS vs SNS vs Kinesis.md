> [!abstract] What is it?
> This section compares **SQS, SNS, and Kinesis**—three core AWS messaging/streaming services—and introduces **Amazon MQ**, which is used for legacy message broker compatibility.

---

## SQS vs SNS vs Kinesis (Core Differences)

### Amazon SQS
**Purpose:** Decouple services using a **queue**  
**Model:** Pull‑based, point‑to‑point  

- Consumers poll messages
- Messages are stored durably
- Each message is processed by **one consumer**
- Handles traffic spikes by buffering
- Supports Standard and FIFO queues

**Best for:** Background jobs, work queues, async processing

---

### Amazon SNS
**Purpose:** Event notifications and **fan‑out**  
**Model:** Push‑based, one‑to‑many  

- Publishers send messages to a topic
- SNS pushes messages to all subscribers
- No long‑term message storage
- Often combined with SQS for durability

**Best for:** Event‑driven architectures, notifications, fan‑out

---

### Amazon Kinesis
**Purpose:** Real‑time **streaming data**  
**Model:** Ordered, replayable streams  

- High‑throughput ingestion
- Multiple consumers read the same data
- Data retention and replay supported
- Used for analytics and real‑time processing

**Best for:** Clickstreams, logs, IoT, real‑time analytics

---

## Comparison Summary

| Feature | SQS | SNS | Kinesis |
|---|---|---|---|
| Communication | One‑to‑one | One‑to‑many | Many‑to‑many |
| Delivery | Pull | Push | Pull |
| Persistence | Yes | No | Yes |
| Replay | No | No | Yes |
| Ordering | FIFO option | No | Per partition |
| Use Case | Work queues | Notifications | Streaming data |

---

## Amazon MQ Overview

> [!info] What is it?
> **Amazon MQ** is a managed **message broker service** for applications that require **traditional messaging protocols**.

### Key Characteristics
- Supports **ActiveMQ** and **RabbitMQ**
- Uses standard protocols:
  - JMS
  - AMQP
  - MQTT
  - STOMP
- Runs inside a VPC
- Provides broker‑level features like exchanges and queues

### Why Amazon MQ Exists
- Designed for **legacy applications**
- Enables lift‑and‑shift migrations
- Avoids rewriting apps to use SQS/SNS

### Amazon MQ vs SQS/SNS
- Amazon MQ requires **broker management concepts**
- SQS/SNS are **cloud‑native and serverless**
- Amazon MQ is not as scalable or cost‑efficient for new apps

> [!tip] Exam Tip  
> Use **Amazon MQ** only when the question mentions **existing messaging protocols** or **legacy systems**.  
> For new architectures, prefer **SQS, SNS, or Kinesis**.

---

<span style="float:left">← [[Kinesis Data Streams & Firehose]]</span><span style="float:right">[[Containers on AWS - ECS, Fargate, ECR & EKS]] →</span>
