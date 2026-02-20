> [!abstract] What is it? **Amazon S3** is a highly durable, scalable, and secure **object storage service** used to store and retrieve any amount of data from anywhere.

---

## S3 Overview

S3 stores data as **objects** inside **buckets**. Each object consists of data, metadata, and a unique key. S3 is designed for **11 nines of durability** and scales automatically without capacity planning.

Common use cases include backups, static website hosting, data lakes, and application assets.

---

## Buckets

- Buckets are globally unique
- Defined at the region level
- Objects are stored using key names
- Bucket names appear in URLs

---

## Bucket Policies

Bucket policies are **JSON‑based IAM policies** attached directly to buckets.

Used to:

- Grant public or private access
- Control access across AWS accounts
- Enforce encryption or HTTPS access

---

## Versioning

Versioning keeps **multiple versions** of an object.

- Protects against accidental deletion
- Allows object rollback
- Required for replication
- Deleted objects become **delete markers**

---

## Replication

S3 supports **automatic replication** of objects.

- Same‑Region Replication (SRR)
- Cross‑Region Replication (CRR)
- Requires versioning enabled
- Replicates new objects only
- Used for disaster recovery and compliance

---

## Storage Classes Overview

|Storage Class|Use Case|
|---|---|
|Standard|Frequently accessed data|
|Intelligent‑Tiering|Unknown access patterns|
|Standard‑IA|Infrequent access|
|One Zone‑IA|Infrequent, single AZ|
|Glacier Instant Retrieval|Rare access, milliseconds|
|Glacier Flexible Retrieval|Archive, minutes to hours|
|Glacier Deep Archive|Long‑term archive|

---

## S3 Express One Zone

- Single AZ storage
- Ultra‑low latency
- High request rates
- Designed for performance‑critical workloads
- Lower durability than Standard

---

> [!note] Exam Tip  
> Use **Standard** for active data, **IA** for backups, **Glacier** for archives, and **Express One Zone** for high‑performance workloads.

<br><br>

<span style="float:left">← [[Amazon Route 53]]</span><span style="float:right">[[S3 Advanced]] →</span>