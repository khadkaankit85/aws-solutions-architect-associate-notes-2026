> [!abstract] What is it?
> **AWS Security and Execution Management** focuses on controlling access, enforcing governance, and managing identities across accounts and organizations. These services define who can do what, where, and under which conditions, while enabling centralized control at scale.

---

## AWS Identity and Access Management (IAM)

IAM controls **authentication and authorization** for AWS resources.

### Core concepts
- **Users** represent human identities
- **Groups** organize users for policy assignment
- **Roles** provide temporary credentials for services, applications, or federated users
- **Policies** define permissions using JSON documents

IAM is evaluated on every API request and is the foundation of AWS security.

---

## IAM Policy Types

### Identity‑based policies
Attached to users, groups, or roles.
- Define what actions an identity can perform
- Most common policy type

### Resource‑based policies
Attached directly to resources such as S3 buckets, SNS topics, or SQS queues.
- Define who can access the resource
- Enable cross‑account access without assuming roles

### Permission boundaries
Set a maximum permission limit for IAM roles or users.
- Prevent privilege escalation
- Common in delegated administration models

### Session policies
Applied at role‑assumption time.
- Further restrict permissions for a specific session

---

## IAM Roles vs Resource‑Based Policies

IAM roles grant permissions **to an identity** after it assumes the role.
- Used by AWS services, applications, and federated users
- Credentials are temporary
- Preferred for service‑to‑service access

Resource‑based policies grant permissions **directly on the resource**.
- No role assumption required
- Common for S3, SNS, and SQS cross‑account access

---

## IAM Policy Evaluation Logic

When an API request is made, AWS evaluates policies in a strict order:

1. Explicit deny overrides everything
2. Explicit allow grants access
3. If no allow is found, access is denied by default

All applicable policies are evaluated together, including identity‑based, resource‑based, permission boundaries, and session policies.

---

## AWS Organizations

AWS Organizations enables **multi‑account management**.

### Key features
- Centralized billing
- Account hierarchy using organizational units
- Policy enforcement across accounts

Organizations allow enterprises to scale securely while maintaining governance.

---

## Service Control Policies (SCPs)

SCPs define **maximum permissions** for accounts or organizational units.

- They do not grant permissions
- They restrict what IAM policies can allow
- Applied at the organization level

SCPs are used to enforce guardrails such as blocking certain regions or services.

---

## Tag Policies

Tag policies standardize **resource tagging** across accounts.

- Define required tag keys and values
- Enforce consistency for cost allocation and governance
- Do not grant or deny access directly

---

## IAM Identity Center (formerly AWS SSO)

IAM Identity Center provides **centralized workforce identity management**.

### Capabilities
- Single sign‑on to AWS accounts and applications
- Integration with external identity providers
- Centralized permission assignment

It replaces managing individual IAM users at scale.

---

## AWS Directory Services

Directory Services integrate AWS with **Microsoft Active Directory**.

### Options
- Managed Microsoft AD
- AD Connector
- Simple AD

These services enable Windows authentication, LDAP integration, and enterprise identity federation.

---

## AWS Control Tower

Control Tower automates **secure multi‑account setup**.

### What it provides
- Preconfigured landing zone
- Guardrails using SCPs and Config rules
- Centralized logging and auditing

Control Tower is used to quickly establish a compliant AWS environment.

---

## Mental Model Summary

| Concept | Purpose |
|---|---|
| IAM | Identity and permission control |
| Roles | Temporary access for services and users |
| Resource policies | Resource‑level access control |
| Organizations | Multi‑account governance |
| SCPs | Permission guardrails |
| Tag policies | Tag standardization |
| Identity Center | Centralized workforce access |
| Directory Services | Active Directory integration |
| Control Tower | Automated secure account setup |

---

<span style="float:left">← [[Monitoring & Audit]]</span><span style="float:right">[[AWS Security & Encryption]] →</span>
