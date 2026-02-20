> [!abstract] What is it? **Amazon ElastiCache** is a fully managed, in‑memory data store used to improve application performance by caching frequently accessed data and storing session state.

---

## Why ElastiCache

ElastiCache stores data **in memory**, making reads extremely fast. It reduces load on databases and helps make applications **stateless**, which improves scalability and resilience. AWS manages OS maintenance, patching, backups, and failover.

---

## Database Cache Pattern

1. Application queries the cache
2. **Cache hit**: data returned immediately
3. **Cache miss**: data fetched from RDS
4. Data written to cache for future requests

> [!note] Cache Invalidation  
> Cached data must be invalidated or refreshed to avoid serving stale data.

---

## Session Store Pattern

- User logs in through any application instance
- Session data is stored in ElastiCache
- User can hit a different instance and still be authenticated
- Enables **horizontal scaling** without sticky sessions

---

## Redis vs Memcached

### Redis

- Multi‑AZ with automatic failover
- Read replicas supported
- Data durability using **AOF persistence**
- Backup and restore supported
- Supports advanced data types such as sets and sorted sets

### Memcached

- Multi‑node for partitioning
- No high availability
- No persistence
- No backup or restore
- Multi‑threaded architecture
- Simple key‑value store

---

## Sharding vs Replication

- **Redis**: supports replication for HA and read scaling
- **Memcached**: uses sharding only, no replication

---

## Security

- Redis supports **IAM authentication**
- Redis AUTH token can be configured
- Security groups control network access
- Memcached does not support IAM authentication

---

## Common Caching Patterns

### Lazy Loading

- Data loaded into cache only when requested
- Cache miss triggers DB read and cache write

### Write Through

- Data written to cache and database at the same time
- No stale data
- Often used for session storage with TTL

---

## Redis Use Case

> [!tip] Gaming Leaderboards  
> Redis sorted sets maintain **unique values with ordering**, making them ideal for real‑time leaderboards and ranking systems.

<br><br>

<span style="float:left">← [[RDS Advanced]]</span><span style="float:right">[[Route 53]] →</span>