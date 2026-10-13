# Redis & RabbitMQ Interview Questions and Answers

**Java Backend Engineer | Short English Answers | Grouped by Topic**

## A. Redis Fundamentals and Caching

### Q43. Why do we use Redis?

**Answer:** Redis is an in-memory data store commonly used for caching, distributed coordination, counters, and temporary data. It can reduce database load and improve response times.

### Q44. What is cache penetration?

**Answer:** Cache penetration occurs when requests for nonexistent data repeatedly reach the database. We can mitigate it with short-lived negative caching or Bloom filters.

### Q45. What is cache breakdown?

**Answer:** Cache breakdown occurs when a heavily requested key expires or becomes unavailable, causing many requests to hit the database. We can mitigate it using request coalescing, locks, or controlled cache refresh.

### Q91. What is a cache avalanche?

**Answer:** A cache avalanche happens when many cached entries expire or become unavailable around the same time, sending a surge of requests to the backing service. Randomized expiration, staggered refreshes, and rate limiting can reduce the impact.

### Q93. What is the difference between Redis eviction and expiration?

**Answer:** Expiration removes keys after their configured time-to-live. Eviction removes keys when memory limits are reached according to the configured policy, which may select only keys with expiration or consider all keys.

## B. Redis Persistence and High Availability

### Q92. What are Redis RDB and AOF persistence?

**Answer:** RDB persists point-in-time snapshots, while AOF records write operations for replay. RDB can be compact and fast to restore, whereas AOF can reduce data loss depending on its fsync policy. Redis can also use both.

### Q94. What is the difference between Redis Sentinel and Redis Cluster?

**Answer:** Sentinel monitors Redis instances and supports failover for a primary-replica setup. Redis Cluster shards data across nodes and provides partitioning with availability mechanisms.

## C. Distributed Systems and Reliability

### Q46. How do you prevent duplicate message processing?

**Answer:** I use idempotent processing, typically with a unique business key or message ID. I also track processing status and use database constraints when appropriate.

**Runnable example:** `./gradlew runInfrastructureExamples` — see `InfrastructureExamples.java`.

The example illustrates duplicate detection in one process. Production consumers need a durable, shared store or database constraint to coordinate across restarts and instances.

### Q47. What is eventual consistency?

**Answer:** Eventual consistency means replicas or services may temporarily have different states but converge if updates stop and propagation succeeds.

### Q49. What is a distributed lock?

**Answer:** A distributed lock coordinates access to a shared resource across multiple processes or machines. It should use appropriate expiration, ownership checks, and fencing tokens when stale lock holders could cause problems.

### Q50. How do you make an API idempotent?

**Answer:** I use an idempotency key to identify repeated requests, store the processing result, and return the existing result for duplicates instead of executing the operation again.

**Runnable example:** `./gradlew runInfrastructureExamples` — see `InfrastructureExamples.java`.

The in-memory store demonstrates the idea only. A real API should persist idempotency keys and results across processes and restarts.

## D. RabbitMQ Message Delivery and Failure Handling

### Q48. How do you handle a failed message?

**Answer:** I use retries with backoff for transient failures, limit retry attempts, and send messages that cannot be processed to a dead-letter queue for investigation.

### Q95. How do message acknowledgements affect delivery?

**Answer:** A consumer acknowledgement tells the broker that a message was processed and can be removed. If acknowledgement is not received, the broker may redeliver the message, so consumers should be designed to handle duplicates.

### Q96. What are publisher confirms?

**Answer:** Publisher confirms let a producer know whether the broker accepted a published message. They improve delivery reliability but do not by themselves guarantee that a consumer processed the message.

## Quick Review

| Topic | Key idea |
|---|---|
| Redis caching | Reduce database load and response time |
| Cache penetration | Nonexistent data repeatedly reaches the database |
| Cache breakdown | One hot key expires and causes a traffic spike |
| Cache avalanche | Many keys expire or disappear together |
| Expiration vs. eviction | TTL-based removal vs. memory-pressure removal |
| RDB vs. AOF | Snapshots vs. replayable write log |
| Sentinel vs. Cluster | Failover monitoring vs. data sharding and availability |
| Duplicate processing | Use idempotency and durable deduplication |
| Eventual consistency | Temporary differences can converge |
| Distributed lock | Coordinate access across processes or machines |
| API idempotency | Repeated requests return the same logical result |
| Consumer acknowledgement | Confirms successful handling to the broker |
| Publisher confirms | Confirms broker acceptance to the producer |
| Failed messages | Retry transient failures; route persistent failures to a DLQ |

**Interview tip:** Distinguish broker-level delivery guarantees from application-level processing guarantees. Publisher confirms, consumer acknowledgements, retries, and dead-letter queues help with reliability, but idempotent consumers are still important because messages may be redelivered.
