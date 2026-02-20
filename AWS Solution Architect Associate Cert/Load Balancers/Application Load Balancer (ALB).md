> [!abstract] What is it?
> A **Layer 7** load balancer — operates at the HTTP level, not just raw TCP traffic.

---

## How it distributes traffic

| Feature         | Detail                                                  |
| --------------- | ------------------------------------------------------- |
| Across machines | Balances HTTP apps across multiple **Target Groups**    |
| Same machine    | Balances multiple apps on one machine (e.g. containers) |
| Redirects       | HTTP → HTTPS and other redirect rules                   |
| Port mapping    | Redirects to dynamic ports in ECS                       |
|                 |                                                         |

---

## Routing Rules

ALB can route to different target groups based on:
- **URL path** — e.g. `/api/*` goes one place, `/web/*` goes another
- **Hostname** — e.g. `api.myapp.com` vs `app.myapp.com`
- **Query strings** — e.g. `?platform=mobile`

> [!tip] Best Use Case
> ALB is a perfect fit for **microservices** and **container-based** apps (Docker, ECS) because of its flexibility and port mapping feature.

---

## Target Groups

> [!info] What can be a target?
> | Target | Protocol Note |
> |---|---|
> | EC2 Instances (via ASG) | HTTP |
> | ECS Tasks | HTTP |
> | Lambda Functions | HTTP request → JSON event |
> | IP Addresses | Must be **private** IPs |

> [!warning] vs Classic Load Balancer
> With Classic LB you'd need **one per application**. ALB can route to **multiple target groups** from a single load balancer — much more efficient.

> [!note] Health Checks
> Health checks happen at the **target group level**, not the individual instance level.

<br><br>

<span style="float:left">← [[IAM — Identity & Access Management]]</span><span style="float:right">[[Network Load Balancer (NLB)]] →</span>