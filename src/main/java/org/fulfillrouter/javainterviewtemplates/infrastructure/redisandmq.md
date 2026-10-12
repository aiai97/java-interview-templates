Q43. Why do we use Redis?

Answer: Redis is an in-memory data store commonly used for caching, distributed coordination, counters, and temporary data. It can reduce database load and improve response times.

Q44. What is cache penetration?

Answer: Cache penetration occurs when requests for nonexistent data repeatedly reach the database. We can mitigate it with short-lived negative caching or Bloom filters.

Q45. What is cache breakdown?

Answer: Cache breakdown occurs when a heavily requested key expires or becomes unavailable, causing many requests to hit the database. We can mitigate it using request coalescing, locks, or controlled cache refresh.

Q46. How do you prevent duplicate message processing?

Answer: I use idempotent processing, typically with a unique business key or message ID. I also track processing status and use database constraints when appropriate.

Q47. What is eventual consistency?

Answer: Eventual consistency means replicas or services may temporarily have different states but converge if updates stop and propagation succeeds.

Q48. How do you handle a failed message?

Answer: I use retries with backoff for transient failures, limit retry attempts, and send messages that cannot be processed to a dead-letter queue for investigation.

Q49. What is a distributed lock?

Answer: A distributed lock coordinates access to a shared resource across multiple processes or machines. It should use appropriate expiration, ownership checks, and fencing tokens when stale lock holders could cause problems.

Q50. How do you make an API idempotent?

Answer: I use an idempotency key to identify repeated requests, store the processing result, and return the existing result for duplicates instead of executing the operation again.