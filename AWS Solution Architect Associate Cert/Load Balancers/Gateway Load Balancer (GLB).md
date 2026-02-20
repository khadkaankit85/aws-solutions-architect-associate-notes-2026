> [!abstract] What is it? A **Layer 3** load balancer designed to **deploy, scale, and manage third‑party virtual appliances** transparently within a VPC.

---

## When to use Gateway Load Balancer

Gateway Load Balancer is used for **inline traffic inspection** and **network security**.

Common scenarios:

- Firewalls
- IDS and IPS
- Deep packet inspection
- Traffic monitoring
- Third‑party security appliances

> [!tip] Best Use Case  
> Use Gateway Load Balancer when you need **transparent traffic inspection** without modifying applications or client configurations.

---

## How it works

Gateway Load Balancer functions as a **transparent network gateway** between:

- User or source
- Virtual appliance
- Destination application

Traffic flow:

1. User sends traffic toward the application
2. Traffic is intercepted by Gateway Load Balancer
3. Traffic is forwarded to a virtual appliance
4. Appliance inspects or modifies traffic
5. Traffic returns to Gateway Load Balancer
6. Traffic is forwarded to the destination application

Neither the user nor the application is aware of the inspection layer.

---

## Key Characteristics

|Feature|Detail|
|---|---|
|OSI Layer|Layer 3|
|Transparency|No application or client changes|
|Scaling|Automatically scales appliances|
|Management|Centralized appliance fleet|
|Primary Use|Inline security and inspection|

---

## GENEVE Protocol

Gateway Load Balancer uses **GENEVE encapsulation** to forward traffic.

|Item|Value|
|---|---|
|Protocol|GENEVE|
|Port|6081|
|Purpose|Encapsulates original packets for inspection|

GENEVE preserves original packet metadata while routing traffic through appliances.

---

## Target Groups

> [!info] What can be a target?
> 
> |Target|Note|
> |---|---|
> |EC2 Instances|Common for security appliances|
> |IP Addresses|Must be private IPs|

Each target typically represents a **virtual appliance instance**.

---

## Example Use Case

> [!note] Traffic Inspection  
> A company inserts a third‑party firewall between users and applications. Gateway Load Balancer automatically scales firewall instances and routes all traffic through them without changing application code or client routing.

<br><br>

<span style="float:left">← [[Network Load Balancer (NLB)]]</span><span style="float:right">[[Elastic Load Balancer - SAA]] →</span>