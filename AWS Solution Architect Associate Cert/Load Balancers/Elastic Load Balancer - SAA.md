## Sticky Sessions (Session Affinity)

> [!info] Idea  
> Ensures requests from the **same client** are routed to the **same backend target** for the duration of a session.

### How it differs from regular load balancing

- Regular LB: each request can go to **any healthy target**
- Sticky sessions: LB **remembers the client** and reuses the same target

### How it works

1. Client sends request
2. Load balancer selects a target
3. Cookie is added to the response
4. Client sends cookie on next request
5. Same target is used

### Why it is used

- Application state stored **in memory**
- Stateful applications
- No external session store

### Supported Load Balancers

- Application Load Balancer
- Network Load Balancer
- Classic Load Balancer

### Cookie Types

> [!note] Categories
> 
> - **Application-based**
>     - Custom cookie
>     - Duration-based cookie
> - **Load balancer-based**
>     - Managed by ELB

> [!warning] Drawback  
> Can cause **uneven load distribution** and reduced fault tolerance.

---

## Cross Zone Load Balancing

> [!info] Idea  
> Distributes traffic **evenly across all targets in all AZs**, not per AZ.

### Example

**Setup**

- AZ A: 2 instances
- AZ B: 8 instances

**Without Cross Zone**

- Each AZ gets 50% traffic
- AZ A overloaded

**With Cross Zone**

- Traffic spread across all 10 instances
- Equal load per instance

### Defaults

- ALB: Enabled
- Classic LB: Enabled
- NLB: Disabled
- Gateway LB: Disabled

### Cost

- ALB and Classic LB: Free
- NLB and Gateway LB: Inter-AZ traffic charged

---

## ELB SSL and TLS

> [!info] Purpose  
> Provides **in-flight encryption** between clients and the load balancer.

### Key Concepts

- **SSL**: Secure Sockets Layer
- **TLS**: Transport Layer Security
- TLS is the newer version, but commonly called SSL

### How it works

1. Client connects to the load balancer
2. Load balancer presents an **X.509 certificate**
3. Encrypted connection is established
4. Load balancer forwards traffic to EC2 targets

### Certificate Management

- Certificates can be:
    - Created manually
    - Managed using **AWS Certificate Manager**
- Configured on **HTTPS listeners**
- TLS version can be specified

### SNI

> [!note] Server Name Indication  
> Allows multiple SSL certificates on the same load balancer.  
> Client sends hostname, ALB selects the correct certificate.

- Supported by **ALB and NLB**
- Not supported by **Classic LB**

---

## Connection Draining

> [!info] Purpose  
> Allows in-flight requests to complete before a target is removed.

### Behavior

- Stops sending **new requests**
- Existing requests are allowed to finish
- Time range: **1 to 3600 seconds**
- Can be disabled

### Naming

- Classic LB: **Connection Draining**
- ALB and NLB: **Deregistration Delay**

> [!tip] Exam Tip  
> Set a low value when requests are short-lived.

<br><br>

<span style="float:left">← [[Gateway Load Balancer (GLB)]]</span><span style="float:right">[[Auto Scaling Groups]] →</span>