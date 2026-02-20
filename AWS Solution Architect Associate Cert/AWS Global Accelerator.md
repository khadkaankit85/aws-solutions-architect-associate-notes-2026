> [!abstract] What is it? **AWS Global Accelerator** is a networking service that improves **availability and performance** for global applications by routing user traffic over the **AWS global network** to the closest healthy endpoint.

## High‑Level Overview

Global Accelerator provides **static anycast IP addresses** that act as a fixed entry point for your application. User traffic enters the AWS edge closest to them and is carried over the **AWS private backbone** to the optimal regional endpoint.

Unlike CloudFront, Global Accelerator does **not cache content**. It accelerates **TCP and UDP traffic** for applications that require low latency and fast failover.

## How it works

- You create an accelerator with **two static IP addresses**
- Clients connect to the nearest AWS edge location
- Traffic is routed over AWS’s global network
- Requests are sent to the **closest healthy endpoint**
- Health checks continuously monitor endpoints
- Automatic failover occurs if an endpoint becomes unhealthy

## Supported Endpoints

Global Accelerator can route traffic to:

- Application Load Balancers
- Network Load Balancers
- EC2 instances
- Elastic IP addresses

## Traffic Flow

1. Client connects to the accelerator IP
2. AWS edge location receives the request
3. Traffic travels over AWS backbone
4. Routed to the optimal regional endpoint
5. Response follows the same optimized path

## Performance Benefits

- Lower latency than public internet routing
- Reduced packet loss and jitter
- Consistent performance for global users

## Availability and Failover

- Continuous health checks
- Automatic regional failover
- No DNS changes required
- Failover happens in seconds

## Global Accelerator vs CloudFront

- **Global Accelerator**: network acceleration, no caching, TCP/UDP
- **CloudFront**: content caching, HTTP/HTTPS only

## Use Cases

- Gaming backends
- VoIP and real‑time communication
- Global APIs
- Multi‑region applications requiring fast failover

> [!note] Exam Tip  
> Use **Global Accelerator** when you need **static IPs**, **fast failover**, and **non‑HTTP traffic** acceleration.

<br><br>

<span style="float:left">← [[Amazon CloudFront]]</span><span style="float:right">[[AWS Storage Extra]] →</span>