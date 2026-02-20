> [!abstract] What is it? **S3 Advanced** features extend Amazon S3 with automation, analytics, performance optimization, and large‑scale data operations.

---

## Lifecycle Rules

Lifecycle rules automate object transitions and deletions.

Used to:

- Move objects between storage classes
- Expire objects after a defined time
- Reduce storage costs automatically

Common transitions:

- Standard → Standard‑IA
- Standard‑IA → Glacier
- Glacier → Deep Archive

---

## S3 Analytics

S3 Analytics helps identify objects that should be moved to **Standard‑IA**.

- Analyzes access patterns
- Generates recommendations
- Does not support One Zone‑IA or Glacier
- Used only for **cost optimization**

---

## Requester Pays

With **Requester Pays**, the requester pays for:

- Data transfer
- Requests

Used when:

- Sharing large datasets publicly
- Data owner wants to avoid access costs

---

## Event Notifications

S3 can send events when actions occur.

Supported destinations:

- Amazon SNS
- Amazon SQS
- AWS Lambda

Common events:

- Object created
- Object deleted

---

## Performance Optimization

S3 automatically scales for high request rates.

Best practices:

- Use random prefixes for keys
- Use multipart uploads for large objects
- Parallelize reads and writes

---

## Batch Operations

S3 Batch Operations perform actions on **millions of objects**.

Supported actions:

- Copy objects
- Replace metadata
- Restore from Glacier
- Invoke Lambda functions

---

## S3 Storage Lens

S3 Storage Lens provides **organization‑wide visibility**.

Features:

- Storage usage metrics
- Activity trends
- Cost optimization insights
- Account and bucket‑level views

---

<br><br>

<span style="float:left">← [[Amazon S3]]</span><span style="float:right">[[S3 Security]] →</span>