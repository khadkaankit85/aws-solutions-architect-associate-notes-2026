> [!abstract] What is it? **S3 Security** = encryption + access control + audit + governance controls to protect objects in buckets.

## Encryption

### Server-side encryption

- **SSE-S3**: AWS-managed keys (simple, default-style encryption).
- **SSE-KMS**: KMS key controls + audit trail (CloudTrail), key policies, grants—use when you need governance.
- **SSE-C**: You provide the key per request (AWS doesn’t store it)—rare in AWS exams vs SSE-KMS.

### Default encryption

- Bucket-level setting to automatically encrypt **new objects** (commonly SSE-S3 or SSE-KMS).
- Often paired with a bucket policy to **deny uploads** that don’t use the required encryption.

### Encryption in transit

- Use **HTTPS (TLS)** for uploads/downloads to protect data over the network.

## CORS

**CORS** controls which browser-based origins can call S3 directly.

- Needed when a web app on `app.example.com` fetches/uploads to `bucket.s3...`
- Config defines allowed **origins**, **methods** (GET/PUT), **headers**, and whether credentials are allowed.

## MFA delete

Extra protection for destructive actions:

- Requires MFA to **permanently delete versions** and to **suspend versioning**
- Works only with **versioning enabled**
- Typically configured/used via CLI/API (not the normal console flow)

## Access logging

### Server access logs

- Writes detailed request logs (who/what/when) into a **target S3 bucket**
- Useful for audit trails and investigations (can be high volume)

## Pre-signed URLs

Temporary, permission-scoped access to an object without making it public.

- **Download**: share a time-limited GET link
- **Upload**: allow a client to PUT directly to S3
- Access is limited by **expiry** and the signer’s permissions

## Object Lock

> [!info] Purpose Prevent deletion/overwrite to meet compliance (WORM—write once, read many).

### Requirements

- **Versioning must be enabled**
- Must enable **Object Lock** at bucket creation (governance feature)

### Retention modes

- **Governance mode**: most users can’t delete/overwrite; privileged users with special permission can bypass.
- **Compliance mode**: **no one** can delete/overwrite until retention expires (strongest).

### Retention types

- **Retention period**: keep until a specific duration passes (e.g., 7 years).
- **Legal hold**: indefinite hold (no expiry) until explicitly removed (independent of retention period).

### What it protects against

- Accidental deletes
- Malicious deletes (especially in Compliance mode)
- Ransomware-style “delete/overwrite” attempts

## Access points

Dedicated access entry to a bucket with its own policy.

- Simplifies managing different access patterns (team/app-specific)
- Can restrict access to specific **VPCs** (common for private/internal access)
- Cleaner than one giant bucket policy for many consumers

## S3 Object Lambda

Transforms objects **at read time** using Lambda—no need to store multiple copies.

- Examples: redact PII, filter fields, convert formats, watermark images
- Client requests object → S3 invokes Lambda → returns transformed response

<span style="float:left">← [[S3 Advanced]]</span><span style="float:right">[[Amazon CloudFront]] →</span>