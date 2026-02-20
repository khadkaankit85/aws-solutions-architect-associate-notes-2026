> [!abstract] What is it?
> **Amazon SNS (Simple Notification Service)** is a fully managed **publish–subscribe (pub/sub)** messaging service that enables one‑to‑many communication between distributed systems.

## Overview
SNS allows producers to publish messages to a **topic**, and multiple subscribers receive those messages simultaneously. It is designed for **fan‑out**, event notifications, and decoupling services that need to react to the same event.

SNS is serverless, highly available, and scales automatically.

---

## Core Concepts

### Topics
A **topic** is a logical access point for publishing messages.
- Producers publish messages to a topic
- Subscribers receive copies of each message

### Publishers
- Applications, Lambda, CloudWatch, S3, EventBridge
- Publish once, SNS delivers to all subscribers

### Subscribers
Supported subscription types:
- SQS
- Lambda
- HTTP/HTTPS endpoints
- Email / SMS
- Mobile push notifications

---

## Message Delivery
- Messages are **pushed** to subscribers (not polled)
- Each subscriber receives its own copy
- Delivery retries are handled by SNS
- Messages are not stored long‑term (unlike SQS)

---

## SNS vs SQS
| SNS | SQS |
|---|---|
| Push‑based | Pull‑based |
| One‑to‑many | One‑to‑one |
| Event notifications | Work queues |
| No message persistence | Durable storage |

---

## Fan‑Out Pattern (SNS + SQS)

> [!info] Pattern
> **SNS fan‑out** allows a single message to be delivered to **multiple SQS queues** in parallel.

### How it works
1. Producer publishes a message to an SNS topic
2. SNS pushes the message to multiple SQS queues
3. Each queue has its own consumers
4. Each consumer processes independently

### Why it’s powerful
- Decouples services completely
- Each consumer can scale independently
- Failure in one consumer does not affect others
- Enables multiple workflows from one event

### Common use cases
- Order placed → billing, inventory, notifications
- File uploaded → processing, indexing, auditing
- Event‑driven microservices

---

## Reliability and Durability
- SNS is highly available across AZs
- Supports delivery retries
- Can integrate with **dead‑letter queues (DLQ)** via SQS

---

## Security
- IAM policies control publish/subscribe permissions
- Supports encryption at rest using KMS
- HTTPS endpoints use TLS for in‑flight encryption

---

> [!tip] Exam Tip  
> Use **SNS + SQS fan‑out** when multiple services must react to the same event **independently and reliably**.

<span style="float:left">← [[SQS]]</span><span style="float:right">[[Kinesis Data Streams & Firehose]] →</span>
