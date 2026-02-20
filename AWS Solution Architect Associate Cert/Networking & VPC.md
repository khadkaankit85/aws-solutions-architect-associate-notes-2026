> [!abstract] What is it?
> **AWS Networking and VPC** services define how resources communicate, how traffic is routed and secured, and how on‑premises networks connect to AWS. These components form the foundation for isolation, connectivity, and network‑level security.

---

## CIDR and IP addressing
CIDR blocks define the IP address range for a VPC.

- IPv4 CIDR ranges are private by default
- Subnets carve smaller CIDR ranges from the VPC
- CIDR planning is critical because ranges cannot be easily changed later

Private IPs are used for internal communication inside the VPC. Public IPs allow resources to be reachable from the internet when routing and gateways permit it.

---

## Default VPC
Every AWS account includes a default VPC.

- One VPC per region
- Public subnets in each AZ
- Internet gateway attached
- Route tables configured for internet access

The default VPC simplifies getting started but is rarely used for production due to limited control and security isolation.

---

## Subnets
Subnets divide a VPC into smaller networks.

- Each subnet exists in a single AZ
- Public subnets route traffic to an internet gateway
- Private subnets do not have direct internet routes

Subnet design determines where workloads can be placed and how they communicate.

---

## Internet Gateway
An internet gateway enables communication between a VPC and the public internet.

- Required for public IPv4 access
- Attached at the VPC level
- Works with route tables to allow ingress and egress

Without an internet gateway, resources cannot reach or be reached from the internet.

---

## Route Tables
Route tables control how traffic flows.

- Each subnet is associated with a route table
- Routes define destination CIDR and target
- Common targets include internet gateways, NAT gateways, and transit gateways

Routing determines whether traffic stays internal or exits the VPC.

---

## Bastion Hosts
A bastion host is a hardened EC2 instance used for administrative access.

- Placed in a public subnet
- Used to access private instances via SSH or RDP
- Requires strict security group rules

Bastion hosts reduce exposure of private resources.

---

## NAT Instances and NAT Gateways
NAT allows private subnets to access the internet without being reachable from it.

### NAT Instances
- EC2‑based
- Require manual scaling and patching
- Single point of failure unless engineered carefully

### NAT Gateways
- Managed and highly available
- Automatically scale
- Preferred for production workloads

---

## Network ACLs and Security Groups
These provide network‑level security.

### Security Groups
- Stateful
- Attached to ENIs
- Allow rules only

### Network ACLs
- Stateless
- Applied at subnet level
- Allow and deny rules

Security groups protect instances, while NACLs protect subnets.

---

## VPC Peering
VPC peering connects two VPCs directly.

- Traffic stays on the AWS network
- No transitive routing
- CIDR ranges must not overlap

Peering is simple but does not scale well for many VPCs.

---

## VPC Endpoints
VPC endpoints allow private access to AWS services.

- Gateway endpoints for S3 and DynamoDB
- Interface endpoints for most other services
- Eliminate the need for internet or NAT access

Endpoints improve security and reduce data transfer costs.

---

## VPC Flow Logs
Flow logs capture IP traffic metadata.

- Source and destination IPs
- Ports and protocols
- Accept or reject status

They are used for troubleshooting, auditing, and security analysis.

---

## Athena with Flow Logs
Flow logs stored in S3 can be queried using Athena.

- Enables SQL analysis of network traffic
- Useful for identifying anomalies and access patterns
- No infrastructure to manage

---

## Site‑to‑Site VPN
Site‑to‑site VPN connects on‑premises networks to AWS.

- Uses IPsec tunnels
- Terminates at a virtual private gateway
- Customer gateway represents on‑prem device

This provides encrypted connectivity over the internet.

---

## Virtual Private Gateway and Customer Gateway
- Virtual private gateway is the AWS side of the VPN
- Customer gateway represents the on‑prem router

Both are required to establish site‑to‑site VPN connectivity.

---

## AWS Direct Connect
Direct Connect provides dedicated private connectivity.

- Bypasses the public internet
- Lower latency and consistent throughput
- Suitable for large data transfers and hybrid architectures

---

## Direct Connect Gateway
A Direct Connect gateway allows a single connection to access multiple VPCs across regions.

- Simplifies multi‑region connectivity
- Reduces operational complexity

---

## Direct Connect plus Site‑to‑Site VPN
VPN can be layered over Direct Connect.

- Provides encryption
- Acts as a backup path
- Improves resilience

---

## Transit Gateway
Transit Gateway acts as a central hub for networking.

- Connects VPCs, VPNs, and Direct Connect
- Supports transitive routing
- Simplifies large network topologies

It replaces complex peering meshes.

---

## VPC Traffic Mirroring
Traffic mirroring copies network traffic to monitoring appliances.

- Used for intrusion detection
- Supports security analysis tools
- Operates at the ENI level

---

## IPv6 in VPC
VPCs support IPv6 addressing.

- Public by default
- No NAT required
- Dual‑stack architectures supported

---

## Egress‑Only Internet Gateway
Egress‑only gateways allow outbound IPv6 traffic.

- Prevent inbound connections
- IPv6 equivalent of NAT for outbound‑only access

---

## Networking Costs in AWS
Costs are driven by data transfer.

- Intra‑AZ traffic is cheapest
- Inter‑AZ traffic incurs charges
- Internet egress is the most expensive

Architectures should minimize unnecessary data movement.

---

## AWS Network Firewall
Network Firewall provides managed network‑level protection.

- Stateful and stateless inspection
- Centralized rule management
- Integrated with VPC routing

It protects against network‑based threats at scale.


<span style="float:left">← [[Security & Encryption]]</span><span style="float:right">[[Disaster Recovery & Migration]] →</span>
