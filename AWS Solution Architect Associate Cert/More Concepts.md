> [!abstract] What is it?
> **More Concepts** covers cross‑cutting architectural ideas that appear repeatedly across AWS designs. These topics are less about individual services and more about understanding patterns, trade‑offs, and system behavior at scale.

---

## Event Processing in AWS
Event processing is the pattern of reacting to changes or actions rather than polling or running on schedules.

Events can originate from services such as S3, DynamoDB, CloudTrail, or applications. These events are routed through services like EventBridge, SNS, or SQS and processed by consumers such as Lambda, ECS tasks, or Step Functions.

This model enables loosely coupled systems where producers and consumers evolve independently, improves scalability, and reduces idle compute.

---

## Caching Strategies in AWS
Caching improves performance and reduces load on backend systems by storing frequently accessed data closer to consumers.

AWS supports caching at multiple layers:
- Application‑level caching using ElastiCache
- Database caching using read replicas or DAX
- Edge caching using CloudFront

Effective caching reduces latency, lowers cost, and increases system resilience during traffic spikes.

---

## Blocking an IP Address in AWS
IP blocking can be enforced at different layers depending on scope and intent.

- Security groups restrict traffic at the instance level
- Network ACLs apply subnet‑level allow and deny rules
- AWS WAF blocks malicious IPs at the application layer
- Route tables and gateways control reachability

Choosing the correct layer avoids unnecessary exposure while maintaining flexibility.

---

## High Performance Computing on AWS
HPC workloads require massive parallelism, low latency networking, and high throughput storage.

AWS supports HPC using:
- Compute‑optimized EC2 instances
- Placement groups for low‑latency networking
- Elastic Fabric Adapter for high‑bandwidth communication
- Parallel file systems such as FSx for Lustre

These capabilities allow scientific simulations, financial modeling, and large‑scale analytics to run efficiently in the cloud.

---

## EC2 Instance High Availability
High availability on EC2 is achieved through redundancy and automation rather than individual instance reliability.

Common techniques include:
- Deploying instances across multiple AZs
- Using Auto Scaling groups for replacement
- Placing load balancers in front of instances
- Designing stateless applications

Failures are expected and handled automatically rather than prevented.

---

<span style="float:left">← [[Disaster Recovery & Migration]]</span><span style="float:right">[[Other Services]] →</span>
