> [!abstract] What is it? **Amazon RDS** is a fully managed relational database service that lets you create and run SQL databases in the cloud without managing the underlying infrastructure.

---

## Overview

RDS supports common relational engines including **PostgreSQL, MySQL, MariaDB, Oracle, Aurora, and IBM Db2**. AWS manages provisioning, operating system patching, backups, monitoring, and maintenance so you can focus on your application.

---

## Why RDS instead of self-managed databases

With self-managed databases, you handle OS patching, backups, scaling, monitoring, and failover. RDS automates these tasks and provides built-in reliability features such as **continuous backups**, **monitoring dashboards**, **maintenance windows**, and **high availability options**.

---

## Storage and Scaling

RDS storage is backed by **EBS** and supports **storage auto scaling**. When free storage drops below a threshold, RDS automatically increases storage up to a configured maximum. This prevents outages caused by running out of disk space.

---

## Read Replicas

Read replicas are used for **read scalability**, not availability. You can create up to **15 read replicas** within the same AZ, across AZs, or across regions.

- Replication is **asynchronous**
- Reads are **eventually consistent**
- Replicas can be **promoted** to standalone databases
- Only supports **SELECT** queries

> [!note] Use Case  
> A production database is under heavy load. A reporting or analytics workload is moved to a read replica so the primary database remains unaffected.

### Cost

- Same-region replication is **free**, even across AZs
- Cross-region replication incurs **network charges**

---

## Multi-AZ

Multi-AZ is designed for **disaster recovery**, not scaling.

- Synchronous replication to a standby instance
- Single DNS endpoint
- Automatic failover if the primary AZ fails
- No application changes required

> [!warning] Not for Scaling  
> Multi-AZ does not improve read performance.

### Enabling Multi-AZ

You can convert a single-AZ database to Multi-AZ with **no downtime**. RDS takes a snapshot, restores it to a standby instance, and establishes synchronous replication.

---

## RDS Custom

RDS Custom is available for **Oracle and Microsoft SQL Server** and provides more control than standard RDS.

### RDS vs RDS Custom

- **RDS**: AWS manages OS and database fully
- **RDS Custom**: You get access to the OS and database
- Allows custom patches, native features, and direct EC2 access
- Automation can be paused to perform custom operations

> [!tip] Exam Tip  
> Use **RDS** for simplicity and automation. Use **RDS Custom** only when you need OS or database-level control.

<br><br>

<span style="float:left">← [[Auto Scaling Groups]]</span><span style="float:right">[[Amazon Aurora]] →</span>