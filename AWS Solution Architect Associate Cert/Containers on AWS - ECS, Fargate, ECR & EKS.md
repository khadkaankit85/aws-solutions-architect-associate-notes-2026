> [!abstract] What is it?
> **Containers on AWS** provide a way to package applications with their dependencies and run them in a scalable, managed environment. For the SAA exam, the key services are **ECS**, **EKS**, **Fargate**, **ECR**, and higher‑level abstractions like **App Runner**.

---

## Amazon ECS (Elastic Container Service)

### Overview
ECS is AWS’s **native container orchestration service**. It manages the scheduling, placement, and lifecycle of containers without requiring you to manage Kubernetes.

You define how containers should run, and ECS handles starting, stopping, and restarting them.

---

### ECS Cluster
An **ECS cluster** is a logical grouping of compute capacity where containers run.

- Can use **EC2 instances** or **Fargate**
- Spans multiple AZs
- Provides isolation and resource management

---

### ECS Task and Task Definition
- A **task definition** is a blueprint for running containers
- Defines:
  - Container image
  - CPU and memory
  - Networking
  - IAM role
- A **task** is a running instance of a task definition

---

### ECS Service
An **ECS service** ensures a specified number of tasks are always running.

- Automatically replaces failed tasks
- Integrates with **ALB**
- Supports rolling deployments
- Used for long‑running applications

---

### ECS Auto Scaling
ECS supports **service auto scaling**.

- Scales tasks based on CloudWatch metrics
- Common metrics:
  - CPU utilization
  - Memory utilization
- Works with both EC2 and Fargate launch types

---

### ECS Architecture (Typical)
- ALB receives traffic
- Routes to ECS service
- ECS service runs tasks across AZs
- Tasks pull images from ECR

---

## AWS Fargate

### Overview
Fargate is a **serverless compute engine for containers**.

- No EC2 management
- No capacity planning
- Pay per task runtime
- Works with ECS and EKS

> [!note] SAA Focus  
> Choose **Fargate** when you want to run containers **without managing servers**.

---

## Amazon ECR (Elastic Container Registry)

### Overview
ECR is a **managed Docker image registry**.

- Stores container images
- Integrated with IAM
- Used by ECS, EKS, and App Runner
- Supports image scanning

---

## Amazon EKS (Elastic Kubernetes Service)

### Overview
EKS is a **managed Kubernetes service**.

- AWS manages the control plane
- You manage worker nodes or use Fargate
- Kubernetes‑native APIs and tooling

> [!warning] SAA Perspective  
> EKS is more complex than ECS and is typically chosen for Kubernetes portability or existing K8s expertise.

---

## AWS App Runner

### Overview
App Runner is a **fully managed container application service**.

- Deploy directly from source code or container image
- Automatic scaling
- No infrastructure management
- Ideal for web apps and APIs

---

## App2Container
A migration tool that:
- Analyzes existing applications
- Containerizes them
- Generates ECS or EKS deployment artifacts

---

## Service Comparison (SAA Level)

| Service | Use Case |
|---|---|
| ECS | AWS‑native container orchestration |
| Fargate | Serverless container compute |
| EKS | Managed Kubernetes |
| ECR | Container image registry |
| App Runner | Simplest container app deployment |

---

> [!tip] Exam Tip  
> If the question emphasizes **simplicity and no server management**, choose **ECS with Fargate** or **App Runner**.  
> If it mentions **Kubernetes**, choose **EKS**.

<span style="float:left">← [[SQS vs SNS vs Kinesis]]</span><span style="float:right">[[Serverless Overview — SAA]] →</span>
