> [!abstract] What is it? **Amazon CloudFront** is a global **CDN** that caches and serves content from **edge locations** to reduce latency and offload your origins (S3, ALB, EC2, API Gateway, etc.).

## Core model

- **Distribution:** The CloudFront configuration (domains, origins, caching, security).
- **Edge locations:** Where content is cached close to users.
- **Origin:** The “source of truth” CloudFront fetches from on a cache miss.
- **Cache behavior:** Rules that decide **which origin** to use and **how to cache** (often per path pattern like `/api/*` vs `/static/*`).

## Origins

### ALB as an origin

- Best for **dynamic** or **microservice** backends.
- CloudFront forwards requests to the ALB; ALB then load-balances to targets.
- Typical pattern:
    - `/static/*` → S3 origin (aggressive caching)
    - `/api/*` → ALB origin (minimal caching, forward headers/cookies as needed)

### EC2 as an origin

- CloudFront can point directly to an EC2 instance (public DNS/IP).
- Works, but **ALB is usually preferred** for HA and scaling (multiple instances, health checks, failover).
- Use direct EC2 origin mainly for simple setups or legacy constraints.

## Caching behavior

- **Cache hit:** Served from edge cache (fast, no origin load).
- **Cache miss:** CloudFront fetches from origin, then caches based on TTL/cache rules.
- **Cache key:** What CloudFront uses to decide “same object or not” (commonly includes path + query strings + selected headers/cookies).
    - More included fields ⇒ fewer hits (more unique cache entries).
    - Fewer included fields ⇒ more hits (but risk serving wrong variants if your app varies by those fields).

## Geo restriction

Controls **who can access** your distribution based on viewer country.

- **Allow list:** Only specified countries can access.
- **Block list:** Specified countries are denied.

> [!note] What it is and isn’t **Geo restriction** is a CloudFront access control feature (country-based). It’s not the same as “latency routing”—CloudFront already serves from nearby edges by design.

## Cache invalidation

Used when you need CloudFront to stop serving cached objects **before TTL expires**.

### When you need it

- You updated an object but kept the **same key** (same path/filename).
- You must push changes immediately (e.g., critical JS/CSS fix).

### How it works

- You submit an invalidation for specific paths (e.g., `/app.js`) or patterns (e.g., `/static/*`).
- CloudFront marks cached copies as stale; next request forces a re-fetch from origin.

### Best practice for most apps

- Prefer **versioned object names** (e.g., `app.v123.js`) so you avoid invalidations.
- Use invalidations for exceptions, not as the default deployment mechanism.

<span style="float:left">← [[Amazon CloudFront]]</span><span style="float:right">[[AWS Global Accelerator]] →</span>