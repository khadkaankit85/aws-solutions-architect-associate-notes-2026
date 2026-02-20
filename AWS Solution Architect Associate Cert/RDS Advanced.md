> [!abstract] What is it? **RDS Advanced** features provide backup, restore, security, and connection management capabilities for Amazon RDS and Aurora databases.

---

## Backups

### Automated Backups

- Daily full backup during the backup window
- Transaction logs backed up every **5 minutes**
- Point‑in‑time restore available
- Retention: **1 to 35 days**
- Can be disabled

Aurora automated backups also support **1 to 35 days** retention.

### Manual Snapshots

- Created manually
- Retained **as long as you want**
- Useful for long‑term backups

> [!note] Cost Tip  
> Stopped RDS instances still incur **storage costs**. For long stops, take a snapshot and restore later.

---

## Restore Options

### RDS Restore

- Restore to a **new database**
- Point‑in‑time restore supported

### Restore from S3

- MySQL RDS: restore from backup stored in S3
- Aurora MySQL: restore backup from S3 into a new Aurora cluster

### Aurora Cloning

- Create a new Aurora cluster from an existing one
- Uses **copy‑on‑write**
- Fast and storage‑efficient
- New storage allocated only when data changes

---

## Security

### Encryption at Rest

- Uses **AWS KMS**
- Must be enabled at creation
- Read replicas inherit encryption
- Unencrypted DB cannot be encrypted later without snapshot restore

### Encryption in Transit

- TLS enabled by default
- Uses AWS TLS root certificates

### Authentication

- IAM authentication supported
- No username or password required

### Network Security

- Controlled by **security groups**
- No SSH access except with **RDS Custom**

### Logging

- Database logs can be sent to **CloudWatch Logs**

---

## RDS Proxy

> [!info] What is it? A fully managed database proxy that pools and shares database connections.

### Benefits

- Reduces database load
- Improves scalability
- Improves failover time by up to **66%**
- Highly available and serverless

### Features

- Supports RDS and Aurora
- No application code changes
- Uses IAM authentication
- Credentials stored in **AWS Secrets Manager**
- Accessible only from within a **VPC**

---

<br><br>

<span style="float:left">← [[Amazon Aurora]]</span><span style="float:right">[[ElastiCache]] →</span>