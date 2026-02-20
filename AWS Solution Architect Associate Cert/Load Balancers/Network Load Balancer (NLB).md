
> [!abstract] What is it?
> A **Layer 4** load balancer — operates at the TCP/UDP level, not HTTP. Built for raw speed and scale.

---

## Key Features

| Feature | Detail |
|---|---|
| Protocols | TCP & UDP traffic |
| Performance | Handles **millions of requests per second** |
| Latency | Ultra-low latency |
| Static IP | One static IP per AZ |
| Elastic IP | Supported — great for **IP whitelisting** |

---

## How it works

Similar to ALB — you create **Target Groups** and NLB routes traffic to them. The difference is it operates lower in the network stack so it's much faster but less flexible than ALB.

---

## Target Groups

> [!info] What can be a target?
> | Target | Note |
> |---|---|
> | EC2 Instances | — |
> | IP Addresses | Must be **private** IPs |
> | Application Load Balancer | You can chain ALB behind NLB |

---

> [!note] Health Checks
> Supports **TCP, HTTP, and HTTPS** protocols.

<br><br>

<span style="float:left">← [[Application Load Balancer (ALB)]]</span><span style="float:right">[[Gateway Load Balancer (GLB)]] →</span>