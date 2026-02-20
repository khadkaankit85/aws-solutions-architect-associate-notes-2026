> [!abstract] What is it?
> **Serverless on AWS** means you deploy code and configure integrations—AWS handles provisioning, scaling, and infrastructure operations. For SAA, the core is **Lambda + event sources**, fronted by **API Gateway**, orchestrated by **Step Functions**, and secured with **Cognito** (often backed by **DynamoDB**).

---

## AWS Lambda

### Overview
**Lambda** runs your code in response to events (or direct invocation) and scales automatically by running more concurrent executions. You pay for execution time and resources, not idle capacity.

Common invocation models:
- **Synchronous:** caller waits (API Gateway, ALB, SDK invoke)
- **Asynchronous:** queued and retried by Lambda (S3, SNS, EventBridge)
- **Stream/poll-based:** Lambda polls shards/partitions (DynamoDB Streams, Kinesis)

---

### Core limits and behaviors (SAA-relevant)
- **Timeout:** max 15 minutes per invocation
- **Memory:** configured per function; CPU scales with memory
- **Ephemeral storage:** `/tmp` is available for scratch space (size configurable)
- **Payload sizes:** vary by integration (API Gateway vs direct invoke vs async)—know that large payloads are constrained and you often store large data in S3 and pass pointers
- **Stateless by default:** reuse of execution environment is possible but not guaranteed—persist state externally (DynamoDB, S3, ElastiCache, RDS)

---

### Concurrency and scaling
Concurrency = number of executions running at the same time.

Key controls:
- **Account concurrency limit:** shared pool across functions
- **Reserved concurrency:** hard cap for a function (also guarantees capacity is held back)
- **Provisioned concurrency:** pre-warms execution environments to reduce cold starts (especially for latency-sensitive APIs)

Failure modes to recognize:
- **Throttling:** if concurrency is exhausted, synchronous calls fail fast; async calls may retry/back off depending on source
- **Backpressure:** for stream sources, slow processing increases iterator age/lag

---

### SnapStart
**SnapStart** reduces cold start time for certain runtimes by initializing the function once, taking a snapshot, and restoring from it on cold starts.

SAA takeaways:
- **Best for:** latency-sensitive synchronous workloads (APIs)
- **Not a universal fix:** still consider provisioned concurrency for strict latency SLOs
- **Initialization semantics matter:** anything done at init time is captured—be careful with time-, randomness-, or connection-sensitive init logic

---

## Lambda at the edge

### Lambda@Edge
Runs Lambda code at CloudFront edge locations for **viewer/origin request/response** events.

Use when you need:
- **Dynamic request/response manipulation** at the CDN layer
- **Auth/redirects/header rewrites** that require more flexibility than simple functions

Tradeoffs:
- More operational complexity than CloudFront Functions
- Designed for edge integration with CloudFront behaviors

### CloudFront Functions
Lightweight JavaScript functions that run at the edge, optimized for **very low latency**.

Use when you need:
- **Simple** header/cookie/query rewrites
- URL normalization, redirects, basic auth logic at the edge
- Maximum performance and minimal overhead

Rule of thumb:
- **CloudFront Functions:** simplest, fastest edge logic
- **Lambda@Edge:** more capable edge compute when Functions aren’t enough

---

## Lambda in a VPC

### What changes when you attach a Lambda to a VPC
- Lambda gets **ENIs** in your subnets and uses your VPC routing
- You can reach **private resources** (RDS in private subnets, internal services)

What you must design explicitly:
- **Outbound internet access:** requires NAT (private subnet + NAT) or public subnet routing (rarely recommended)
- **AWS service access without internet:** use **VPC endpoints**
  - **Gateway endpoint:** S3, DynamoDB
  - **Interface endpoints:** many AWS APIs (e.g., Secrets Manager, STS, CloudWatch Logs depending on setup)

Common exam pitfall:
- “Lambda in VPC can’t reach the internet” is not inherently true—it can, but only if you provide NAT/routing.

---

## RDS and Lambda integrations

### Aurora invoking Lambda (database-to-Lambda)
Aurora (MySQL/PostgreSQL variants) can invoke Lambda from within the database engine (used for event-driven workflows from SQL).

SAA framing:
- **Use case:** DB-side triggers/workflows that call external services without app involvement
- **Tradeoff:** pushes logic into the database—powerful but can complicate debugging and coupling

### RDS event notifications
RDS can emit **event notifications** (failover, snapshot, maintenance, etc.) to **SNS**.
Typical pattern:
- **RDS → SNS → Lambda** (or email/SQS/etc.)

---

## Event sources and notifications

### S3 event notifications
S3 can publish events like `ObjectCreated` / `ObjectRemoved` to:
- **Lambda**
- **SQS**
- **SNS**
- **EventBridge**

SAA patterns:
- **S3 → Lambda:** immediate processing (thumbnails, metadata extraction)
- **S3 → SQS → Lambda/EC2:** buffer and control concurrency for bursty uploads

### DynamoDB Streams
Streams capture item-level changes (insert/modify/remove) and can trigger Lambda.

Key points:
- **Near real-time change data capture**
- **Ordering per partition key** (stream shards)
- **Retries:** failed batches can be retried; design idempotent handlers

---

## DynamoDB (advanced features for serverless)

### Capacity modes
- **On-demand:** simplest, auto-scales; great for spiky/unpredictable traffic
- **Provisioned:** set RCU/WCU; can use auto scaling; cheaper at steady high throughput

### Indexing
- **LSI:** same partition key, different sort key (defined at table creation)
- **GSI:** different partition and/or sort key (more flexible; eventual consistency by default)

### Consistency
- **Eventually consistent reads:** default, cheaper
- **Strongly consistent reads:** only on base table (not GSI)

### Streams + Lambda
- Event-driven processing, projections, denormalization, audit pipelines

### Global Tables
- Multi-region, active-active replication for low-latency global apps
- Conflict resolution is last-writer-wins style—design for it

### TTL
- Automatic expiry of items after a timestamp
- Great for sessions, temporary state, dedupe windows

### PITR and backups
- **Point-in-time recovery:** restore to a second within retention window
- **On-demand backups:** manual snapshots

### Transactions and conditional writes
- **Transactions:** all-or-nothing across multiple items/tables
- **Condition expressions:** optimistic concurrency control (prevent overwrites, enforce invariants)

### DAX
- In-memory cache for DynamoDB reads
- Use when you need microsecond read latency and high read throughput without changing app logic much

---

## API Gateway (overview)

### What it is
**API Gateway** is the managed front door for APIs—handles auth, throttling, routing, and integration to backends (Lambda, HTTP services, AWS services).

### REST API vs HTTP API (SAA-level)
- **HTTP API:** simpler, lower latency/cost for many common use cases (Lambda + JWT/OIDC)
- **REST API:** more features (advanced request/response transforms, API keys/usage plans, etc.)

### Core features to know
- **AuthN/AuthZ:** IAM, Cognito authorizers, JWT authorizers (HTTP API), Lambda authorizers
- **Throttling:** protect backends with rate/burst limits
- **Caching:** reduce backend calls for cacheable GETs (REST API feature set)
- **Stages + deployments:** versioned API releases with stage variables
- **Custom domains:** map your domain to API Gateway

---

## Step Functions

### What it is
**Step Functions** orchestrates workflows as state machines—retries, branching, parallelism, timeouts, and error handling without writing glue code.

### Standard vs Express
- **Standard:** long-running, durable workflows with detailed execution history (great for business processes)
- **Express:** high-volume, short-duration workflows (great for event processing)

### Why it matters for SAA
- Replaces “Lambda chaining” with explicit orchestration
- Built-in **retries**, **catch/fallback**, **timeouts**, and **human-readable** workflow logic

Common patterns:
- **Saga-style compensation:** if step 3 fails, run compensating actions for steps 1–2
- **Parallel fan-out:** process multiple tasks concurrently, then join

---

## Amazon Cognito (in depth)

### User Pools (authentication)
User Pools are for **user sign-up/sign-in** and issuing tokens.

Key concepts:
- **JWT tokens:** ID token (user claims), Access token (API authorization), Refresh token (renewal)
- **Hosted UI:** quick OAuth2/OIDC login pages
- **Federation:** integrate with Google/Apple/SAML/OIDC providers
- **MFA:** SMS/TOTP options depending on configuration
- **Triggers:** Lambda hooks (pre-signup, post-confirmation, pre-token generation, etc.) to customize auth flows

Use case:
- “I need login for my app and JWTs for my API” → **User Pool**

### Identity Pools (authorization to AWS)
Identity Pools provide **temporary AWS credentials** (via STS) for users (guest or authenticated).

Key concepts:
- Map users to **IAM roles**
- Grant direct access to AWS services (e.g., upload to S3 from browser/mobile securely)

Use case:
- “Mobile app users should upload to S3 directly” → **Identity Pool** (often with User Pool as the identity provider)

### Cognito + API Gateway
Common SAA pattern:
- **Cognito User Pool authorizer** on API Gateway
- API Gateway validates JWT and forwards claims to Lambda/backend

---

<span style="float:left">← [[Containers on AWS — ECS, Fargate, EKS]]</span><span style="float:right">[[Data & Analytics]] →</span>
