> [!abstract] What is it?
> **AWS Security and Encryption** services protect data at rest, in transit, and in use, while detecting threats and enforcing security controls across accounts and workloads. These services cover encryption, key management, secrets handling, network protection, and continuous security monitoring.

---

## Encryption fundamentals
Encryption protects data by converting it into an unreadable form unless the correct key is provided.

- **At rest**: data stored on disk or in object storage
- **In transit**: data moving across networks using TLS
- **In use**: data protected while being processed, typically via hardware isolation

AWS services integrate encryption by default, but key ownership and access control determine the security posture.

---

## AWS Key Management Service (KMS)
KMS manages cryptographic keys used to encrypt data across AWS services.

KMS keys control who can encrypt and decrypt data through IAM policies and key policies. AWS services such as S3, EBS, RDS, and Lambda integrate directly with KMS so encryption happens transparently while access remains tightly controlled.

### Multi‑Region keys
Multi‑Region KMS keys replicate key material across regions.

- Enable encrypted data replication without re‑encryption
- Used for disaster recovery and global architectures
- Maintain the same key ID across regions

---

## S3 replication with encryption
When S3 objects are replicated across regions, encryption must be compatible.

- SSE‑S3 objects replicate automatically
- SSE‑KMS objects require destination KMS permissions
- Multi‑Region KMS keys simplify cross‑region replication

Replication preserves encryption while maintaining access control boundaries.

---

## Encrypted AMI sharing
Sharing encrypted AMIs requires explicit key access.

- The AMI owner must share the KMS key
- The recipient must have decrypt permissions
- The AMI is copied and re‑encrypted in the target account

This ensures encrypted machine images remain protected across accounts.

---

## AWS Systems Manager Parameter Store
Parameter Store stores configuration values and secrets.

- Supports plaintext and encrypted parameters
- Integrates with KMS for encryption
- Ideal for configuration data and small secrets

It is commonly used for application configuration rather than high‑rotation secrets.

---

## AWS Secrets Manager
Secrets Manager stores and rotates sensitive credentials.

- Designed for passwords, API keys, and database credentials
- Automatic rotation using Lambda
- Fine‑grained access control and auditing

Secrets Manager is preferred when credentials must rotate regularly.

---

## AWS Certificate Manager (ACM)
ACM manages TLS certificates.

- Issues and renews certificates automatically
- Integrates with ALB, CloudFront, and API Gateway
- Eliminates manual certificate management

ACM simplifies encryption in transit for public and internal services.

---

## AWS CloudHSM
CloudHSM provides dedicated hardware security modules.

- Full control over cryptographic keys
- FIPS‑compliant hardware
- Used for regulatory or compliance requirements

CloudHSM is chosen when KMS abstraction is insufficient.

---

## AWS WAF
Web Application Firewall protects HTTP applications.

- Filters malicious requests
- Blocks common exploits such as SQL injection
- Integrates with ALB, API Gateway, and CloudFront

WAF operates at the application layer.

---

## AWS Shield
Shield protects against distributed denial‑of‑service attacks.

- Shield Standard provides automatic protection
- Shield Advanced adds cost protection and response support

Shield focuses on availability protection.

---

## AWS Firewall Manager
Firewall Manager centrally manages security rules.

- Applies WAF, Shield, and security group rules across accounts
- Enforces consistent security policies
- Requires AWS Organizations

It simplifies security governance at scale.

---

## Amazon GuardDuty
GuardDuty detects threats using logs and ML.

- Analyzes CloudTrail, VPC Flow Logs, and DNS logs
- Identifies compromised credentials and malicious activity
- No agents required

GuardDuty provides continuous threat detection.

---

## Amazon Inspector
Inspector assesses workload vulnerabilities.

- Scans EC2 instances and container images
- Identifies missing patches and CVEs
- Integrates with ECR and EC2

Inspector focuses on vulnerability management.

---

## Amazon Macie
Macie discovers and protects sensitive data.

- Scans S3 objects
- Identifies PII and sensitive content
- Generates findings for compliance and security teams

Macie addresses data exposure risk.

---

## Mental model summary

| Area | Service |
|---|---|
| Key management | KMS, CloudHSM |
| Secrets | Parameter Store, Secrets Manager |
| Certificates | ACM |
| App protection | WAF |
| DDoS protection | Shield |
| Central policy | Firewall Manager |
| Threat detection | GuardDuty |
| Vulnerability scanning | Inspector |
| Data classification | Macie |

---

<span style="float:left">← [[Security & Execution]]</span><span style="float:right">[[Networking & VPC]] →</span>
