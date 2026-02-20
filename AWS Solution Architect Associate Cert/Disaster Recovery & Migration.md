> [!abstract] What is it?
> **Disaster Recovery and Migration on AWS** focuses on keeping systems available during failures and moving workloads into AWS safely and efficiently. These services address resilience, data protection, and large‑scale migration from on‑premises or other environments.

---

## Disaster Recovery on AWS

Disaster recovery is about restoring workloads after failures such as outages, data corruption, or regional disruptions. AWS supports multiple recovery strategies depending on cost, complexity, and recovery objectives.

### Core DR strategies
- **Backup and restore**: lowest cost, highest recovery time
- **Pilot light**: minimal core services always running
- **Warm standby**: scaled‑down but functional environment
- **Multi‑site active‑active**: full redundancy with minimal downtime

These strategies balance **RTO** (recovery time objective) and **RPO** (recovery point objective).

---

## AWS Elastic Disaster Recovery
Elastic Disaster Recovery provides continuous replication of servers into AWS.

- Replicates block‑level data from source servers
- Maintains a lightweight staging area
- Launches recovery instances on demand

This service is used to recover on‑premises or cloud workloads quickly without maintaining a full duplicate environment.

---

## AWS Database Migration Service (DMS)
DMS migrates databases with minimal downtime.

- Supports homogeneous and heterogeneous migrations
- Performs full load followed by continuous replication
- Keeps source and target databases in sync during migration

DMS is commonly used to move databases into managed services while applications remain online.

---

## RDS and Aurora Migrations
Relational databases can be migrated into AWS managed engines.

- Native tools and DMS support MySQL, PostgreSQL, Oracle, SQL Server
- Aurora supports migration from compatible engines
- Read replicas and logical replication reduce downtime

These migrations offload operational burden while improving scalability and availability.

---

## On‑Premises to AWS Migration Strategy
Migrating from on‑premises environments typically follows structured phases.

- Discovery and assessment
- Application dependency mapping
- Data migration
- Cutover and validation

AWS migration tools automate much of this process.

---

## AWS Backup
AWS Backup centralizes backup management.

- Supports EBS, RDS, DynamoDB, EFS, FSx
- Policy‑based scheduling and retention
- Cross‑region and cross‑account backups

This service ensures consistent data protection across workloads.

---

## AWS Application Migration Service (MGN)
MGN migrates servers into AWS with minimal downtime.

- Continuous replication at the block level
- Automated conversion to EC2 instances
- Supports physical and virtual servers

MGN is used for large‑scale lift‑and‑shift migrations.

---

## Transferring Large Datasets into AWS
Large data transfers require specialized approaches.

- **AWS Snowball and Snowmobile** for offline transfer
- **Direct Connect** for sustained high‑throughput transfer
- **S3 Transfer Acceleration** for global uploads

Choosing the right method depends on data size, time constraints, and network capacity.

---

## VMware Cloud on AWS
VMware Cloud on AWS runs VMware workloads natively on AWS infrastructure.

- No refactoring required
- Supports hybrid and gradual migration
- Integrates with AWS services

This is used when organizations want to migrate VMware environments without changing application architecture.


<span style="float:left">← [[Networking & VPC]]</span><span style="float:right">[[More Concepts]] →</span>
