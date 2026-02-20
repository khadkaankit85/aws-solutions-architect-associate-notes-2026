> [!abstract] What is it? **Amazon SQS (Simple Queue Service)** is a fully managed **message queue** that decouples producers and consumers, allowing systems to scale independently and reliably.

## Overview

SQS enables asynchronous communication between services. Producers send messages to a queue, and consumers poll the queue to process them. This prevents tight coupling and protects downstream systems from traffic spikes or failures.

---

## Message Flow

- Producer sends a message to the queue
- Message is stored redundantly across AZs
- Consumer polls the queue
- Message is processed
- Message is deleted after successful processing

If not deleted, the message becomes visible again.

---

## Long Polling

Long polling reduces empty responses and cost.

- Consumer waits up to **20 seconds** for messages
- Reduces API calls
- Improves efficiency
- Recommended over short polling

---

## Visibility Timeout

Controls how long a message stays hidden after being read.

- Default: **30 seconds**
- Max: **12 hours**
- If processing fails and message isn’t deleted, it reappears
- Must be longer than processing time

> [!warning] Common Pitfall  
> Too short a visibility timeout causes duplicate processing.

---

## Standard vs FIFO Queues

### Standard Queue

- At‑least‑once delivery
- Best‑effort ordering
- Nearly unlimited throughput
- Used for most workloads

### FIFO Queue

- Exactly‑once processing
- Strict ordering
- Limited throughput
- Requires **Message Group ID**
- Used when order matters (payments, transactions)

---

## Auto Scaling with SQS

SQS integrates with **Auto Scaling Groups**.

- CloudWatch monitors queue depth
- Scale out when messages increase
- Scale in when queue drains
- Enables elastic, event‑driven architectures

> [!tip] Exam Tip  
> SQS buffers traffic so consumers can scale independently without overload.

---

## Reliability

- Messages stored across multiple AZs
- Highly durable
- No infrastructure to manage

---

<br><br>

<span style="float:left">← [[AWS Storage Extra]]</span><span style="float:right">[[SNS]] →</span>