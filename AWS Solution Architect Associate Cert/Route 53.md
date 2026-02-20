> [!abstract] What is it? **Amazon Route 53** is a highly available and scalable **DNS service** that translates domain names into IP addresses and controls how users are routed to resources.

---

## How DNS works

1. User enters a domain in the browser
2. Browser queries the **local DNS resolver**
3. Resolver queries the **Root DNS server**
4. Root points to the **TLD DNS server** (.com, .org)
5. TLD points to the **authoritative DNS server**
6. Authoritative server returns the IP address
7. Browser connects to the web server

---

## Route 53 Basics

- AWS managed **authoritative DNS**
- Customers control DNS records
- Can register domains and manage DNS in one place
- **100% availability SLA**
- Name comes from **DNS port 53**

---

## Hosted Zones

A **hosted zone** is a container for DNS records.

### Public Hosted Zone

- Routes traffic on the public internet
- Used for internet‑facing domains

### Private Hosted Zone

- Routes traffic **within a VPC**
- Used for internal services

> [!note] Cost  
> $0.50 per hosted zone per month

---

## DNS Records

Each record defines how traffic is routed.

Record fields:

- **Name**
- **Type**
- **Value**
- **TTL**
- **Routing policy**

### Must‑Know Record Types

- **A**: hostname → IPv4
- **AAAA**: hostname → IPv6
- **CNAME**: hostname → hostname (not allowed at root)
- **NS**: name servers for hosted zone

---

## TTL

- Controls how long DNS responses are cached
- **Low TTL**: faster updates, more DNS queries
- **High TTL**: fewer queries, slower updates
- Alias records do **not** use TTL

---

## CNAME vs Alias

### CNAME

- Points to another hostname
- Cannot be used at root domain
- Works for non‑AWS resources

### Alias

- AWS‑only extension to DNS
- Works at root and non‑root domains
- Automatically tracks IP changes
- No TTL required

Alias targets include:

- ELB
- CloudFront
- API Gateway
- S3
- VPC interface endpoints

---

## Routing Policies

Routing policies control **DNS responses**, not traffic flow.

### Simple

- Single resource
- Multiple values returned randomly

### Weighted

- Control percentage of traffic per resource
- Weights do not need to total 100
- Used for testing and gradual rollouts

### Latency

- Routes users to the **lowest‑latency region**

### Failover

- Active‑passive setup
- Uses health checks

### Geolocation

- Routes based on user location

### Geoproximity

- Routes based on geographic bias

### IP‑Based

- Routes based on client IP ranges

### Multi‑Value

- Returns multiple healthy records
- Can be associated with health checks

---

## Health Checks

- Monitor endpoint health
- Used with failover and multi‑value routing
- Can monitor AWS and non‑AWS endpoints

---

## Route 53 Resolver

- Enables **hybrid DNS**
- Resolves DNS between on‑prem and AWS
- Supports inbound and outbound endpoints

---

<br><br>

<span style="float:left">← [[Amazon ElastiCache]]</span><span style="float:right">[[Amazon S3]] →</span>