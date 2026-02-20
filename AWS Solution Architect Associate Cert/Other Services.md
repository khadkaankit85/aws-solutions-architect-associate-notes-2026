> [!abstract] What is it?
> **Other AWS Services** covers supporting services that don’t fit neatly into compute, storage, or networking, but are critical for automation, messaging, cost control, and operational efficiency. These services often appear in architectures as glue components that simplify management and integration.

---

## AWS CloudFormation
CloudFormation enables infrastructure to be defined as code using templates.

Resources are described declaratively, and CloudFormation handles creation, updates, and deletion in a controlled manner. Stacks track state and dependencies, allowing repeatable and auditable infrastructure deployments.

CloudFormation is used to standardize environments, reduce configuration drift, and automate complex setups.

---

## CloudFormation Service Role
A service role allows CloudFormation to assume permissions on your behalf.

Instead of granting broad permissions to users, CloudFormation uses this role to create and manage resources. This improves security by limiting who can deploy infrastructure and what actions are allowed.

---

## Amazon SES
Simple Email Service provides scalable email sending.

SES supports transactional and bulk email, integrates with applications through APIs or SMTP, and includes reputation management features. It is commonly used for notifications, alerts, and application‑generated emails.

---

## Amazon Pinpoint
Pinpoint manages user engagement across channels.

It supports email, SMS, push notifications, and analytics. Pinpoint tracks user behavior and campaign effectiveness, making it suitable for targeted messaging and engagement workflows.

---

## AWS Systems Manager Session Manager
Session Manager provides secure shell access to instances without opening inbound ports.

Access is controlled through IAM, sessions are logged, and no bastion hosts or SSH keys are required. This improves security and auditability for instance access.

---

## AWS Systems Manager Other Services
Systems Manager includes multiple operational tools.

- Run Command executes commands remotely
- Patch Manager automates OS patching
- Automation runs operational workflows
- Inventory collects system metadata

Together, these services centralize operational management.

---

## AWS Cost Explorer
Cost Explorer visualizes and analyzes AWS spending.

It breaks down costs by service, account, tag, and time period. This helps teams understand usage patterns and optimize spending.

---

## AWS Cost Anomaly Detection
Cost Anomaly Detection uses machine learning to identify unusual spending.

It monitors historical usage and alerts when costs deviate from expected patterns. This enables early detection of misconfigurations or runaway workloads.

---

## AWS Outposts
Outposts extends AWS infrastructure into on‑premises environments.

It provides consistent APIs and services for hybrid deployments where low latency or data residency is required.

---

## AWS Batch
Batch runs large‑scale batch computing workloads.

It provisions compute resources automatically, schedules jobs, and optimizes cost by selecting appropriate instance types. Batch is used for data processing, simulations, and offline workloads.

---

## AWS AppFlow
AppFlow transfers data between SaaS applications and AWS services.

It supports scheduled or event‑driven flows and requires no custom code. AppFlow simplifies data ingestion from external systems.

---

## AWS Amplify
Amplify accelerates frontend and mobile application development.

It provides hosting, authentication, APIs, and CI/CD integration. Amplify abstracts backend complexity for client‑side developers.

---

## Instance Scheduler on AWS
Instance Scheduler automates start and stop schedules for EC2 and RDS.

It uses tags and schedules to reduce costs by running resources only when needed. This is commonly used for non‑production environments.

---

<span style="float:left">← [[More Concepts]]</span><span style="float:right">[[Architectures]] →</span>
