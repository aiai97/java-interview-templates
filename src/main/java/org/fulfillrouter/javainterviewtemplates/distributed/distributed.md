# Distributed Systems Interview Questions and Answers

**Java Backend Engineer | Short English Answers | Ordered by Interview Frequency**

## A. Distributed Systems Fundamentals

**Q1. What is a distributed system?**  
Answer: A distributed system consists of multiple independent computers that communicate over a network and work together as one system.

**Q2. Why are distributed systems difficult to design?**  
Answer: They must handle network failures, partial failures, concurrency, data consistency, and unpredictable communication delays.

**Q3. What is a partial failure?**  
Answer: A partial failure occurs when some components fail while the rest of the system continues to operate.

**Q4. What is the CAP theorem?**  
Answer: During a network partition, a distributed system must trade off between consistency and availability. Partition tolerance is necessary when network partitions must be handled.

**Q5. What are the three properties in CAP?**  
Answer: Consistency means every successful read observes the latest completed write. Availability means every request to a non-failing node receives a response. Partition tolerance means the system continues operating despite network communication failures.

**Q6. Can a distributed system guarantee consistency, availability, and partition tolerance simultaneously?**  
Answer: Not during a network partition. The system must choose whether to reject or delay some requests to preserve consistency, or respond while potentially returning stale data.

**Q7. What is the difference between CAP consistency and ACID consistency?**  
Answer: CAP consistency concerns whether distributed reads observe a single consistent view of data. ACID consistency means a transaction preserves database-defined rules and constraints.

**Q8. What is the BASE model?**  
Answer: BASE stands for Basically Available, Soft State, and Eventual Consistency. It describes systems that favor availability and allow temporary inconsistencies.

**Q9. What is eventual consistency?**  
Answer: Eventual consistency means replicas converge to the same value if no new updates occur and updates are eventually propagated successfully.

**Q10. What is strong consistency?**  
Answer: Strong consistency ensures that reads observe the latest completed write according to the system's consistency guarantees.

**Q11. What is the difference between synchronous and asynchronous communication?**  
Answer: Synchronous communication waits for a response before proceeding. Asynchronous communication allows the sender to continue while the receiver processes the request later.

**Q12. What is a distributed system's biggest challenge compared with a single-machine system?**  
Answer: Communication between machines can fail or be delayed independently, so the system cannot assume that every request receives a timely response.

## B. Consistency Models

**Q13. What is linearizability?**  
Answer: Linearizability makes each operation appear to take effect atomically at some point between its invocation and response, while respecting real-time ordering.

**Q14. What is the difference between linearizability and eventual consistency?**  
Answer: Linearizability provides a single real-time-consistent view of operations. Eventual consistency allows temporary differences between replicas.

**Q15. What is sequential consistency?**  
Answer: Sequential consistency means operations appear in one global sequential order that preserves each individual process's program order, but not necessarily real-time order.

**Q16. What is causal consistency?**  
Answer: Causal consistency guarantees that causally related operations are observed in the same order by all nodes.

**Q17. What is read-your-writes consistency?**  
Answer: It guarantees that a client can observe its own successful writes in subsequent reads.

**Q18. What is stale data?**  
Answer: Stale data is data that does not reflect the latest update, often because a replica or cache has not yet received the change.

**Q19. Why might a read from a database replica return stale data?**  
Answer: With asynchronous replication, the primary may commit a write before the replica receives and applies it.

**Q20. How can you reduce stale reads?**  
Answer: Use synchronous replication where appropriate, route critical reads to the primary, or wait until the replica has applied the required update.

## C. Failures, Timeouts, and Reliability

**Q21. Why are timeouts important in distributed systems?**  
Answer: Timeouts prevent requests from waiting indefinitely when a remote service is slow or unreachable.

**Q22. What is a network partition?**  
Answer: A network partition occurs when groups of nodes cannot communicate reliably with one another.

**Q23. Why is retrying a failed request dangerous?**  
Answer: The original request may have succeeded even if its response was lost. Retrying can execute the same operation more than once.

**Q24. How do you implement retries safely?**  
Answer: Retry transient failures with bounded attempts, exponential backoff, jitter, and idempotent operations.

**Q25. What is exponential backoff?**  
Answer: Exponential backoff increases the delay between retries exponentially, reducing pressure on an overloaded service.

**Q26. Why add jitter to retry delays?**  
Answer: Jitter randomizes retry timing so many clients do not retry simultaneously and overload the service again.

**Q27. What is idempotency?**  
Answer: An operation is idempotent if repeating it produces the same intended effect as executing it once.

**Q28. How do you prevent duplicate order creation?**  
Answer: Use an idempotency key and enforce a unique business constraint in the database. Return the existing result for duplicate requests.

**Q29. What is a circuit breaker?**  
Answer: A circuit breaker temporarily blocks calls to an unhealthy service to prevent repeated failures and allow recovery.

**Q30. What are the states of a typical circuit breaker?**  
Answer: Closed allows requests, open blocks requests, and half-open permits limited test requests to check whether the service has recovered.

**Q31. What is bulkheading?**  
Answer: Bulkheading isolates resources, such as thread pools or connection pools, so a failure in one component does not exhaust resources needed by others.

**Q32. What is graceful degradation?**  
Answer: Graceful degradation keeps essential functionality available when non-critical services fail, possibly with reduced features.

**Q33. What is backpressure?**  
Answer: Backpressure limits incoming work when a consumer cannot process requests as quickly as they arrive.

**Q34. What is the difference between at-most-once and at-least-once delivery?**  
Answer: At-most-once delivery avoids redelivery but may lose messages. At-least-once delivery retries until acknowledged but may deliver duplicates.

**Q35. Can a distributed system guarantee exactly-once processing?**  
Answer: End-to-end exactly-once effects are difficult. Systems combine delivery guarantees with idempotency, durable state, and transactional coordination to prevent duplicate business effects.

## D. Distributed Transactions

**Q36. Why are distributed transactions difficult?**  
Answer: A business operation may span multiple services or databases that can fail independently, and there may be no single local transaction covering all of them.

**Q37. What is Two-Phase Commit (2PC)?**  
Answer: A coordinator first asks participants to prepare, then tells them to commit or abort. It can preserve atomicity but may block if the coordinator or participants fail.

**Q38. What happens during the prepare phase of 2PC?**  
Answer: Each participant checks whether it can commit, performs the required preparation, and votes yes or no without making the final decision independently.

**Q39. What is the Saga pattern?**  
Answer: Saga breaks a long-running distributed transaction into local transactions, each with a compensating action for handling failures.

**Q40. What is a compensating transaction?**  
Answer: A compensating transaction performs a business action that counteracts an earlier completed action, such as refunding a payment.

**Q41. What is TCC?**  
Answer: TCC stands for Try, Confirm, and Cancel. Services reserve resources during Try, finalize them during Confirm, or release them during Cancel.

**Q42. What is the Transactional Outbox pattern?**  
Answer: The application writes business data and an event record in the same database transaction. A separate publisher sends the event to the message broker.

**Q43. How do you maintain consistency between a database and a message queue?**  
Answer: Use a Transactional Outbox or another reliable publication mechanism, then make consumers idempotent because messages may be delivered more than once.

**Q44. When would you choose Saga over 2PC?**  
Answer: Saga is often better for long-running workflows across independent services where eventual consistency and compensation are acceptable. 2PC is suitable when atomic commitment is required and all participants support it.

## E. Replication, Sharding, and High Availability

**Q45. What is database replication?**  
Answer: Replication copies data from one database node to other nodes to improve availability, read scalability, or fault tolerance.

**Q46. What is the difference between synchronous and asynchronous replication?**  
Answer: Synchronous replication waits for acknowledgements from designated replicas before confirming a write. Asynchronous replication confirms earlier but may lose recent writes during failures.

**Q47. What is database sharding?**  
Answer: Sharding splits a dataset across multiple database nodes so each node stores only part of the data.

**Q48. What is the difference between replication and sharding?**  
Answer: Replication copies the same data to multiple nodes. Sharding distributes different subsets of data across nodes.

**Q49. What is consistent hashing?**  
Answer: Consistent hashing maps keys and nodes onto a hash ring, so adding or removing a node typically remaps only a portion of the keys.

**Q50. What is automatic failover?**  
Answer: Automatic failover promotes or routes traffic to a healthy node when the current primary or active node is considered unavailable.

**Q51. What is quorum?**  
Answer: A quorum is a minimum number of node responses required to make a decision or complete an operation under a system's protocol.

**Q52. How can you handle stale reads from replicas?**  
Answer: Route critical reads to the primary, wait for replication progress, or use a consistency mechanism supported by the database.

**Q53. What is data rebalancing?**  
Answer: Data rebalancing redistributes data or workload when nodes are added, removed, or become overloaded.

**Q54. What is the difference between horizontal and vertical scaling?**  
Answer: Vertical scaling adds resources to one machine. Horizontal scaling adds more machines or instances.

## F. Consensus and Leader Election

**Q55. What is distributed consensus?**  
Answer: Distributed consensus allows multiple nodes to agree on a value or decision despite certain node or network failures.

**Q56. What problem does Raft solve?**  
Answer: Raft is a consensus algorithm that helps a cluster agree on an ordered log of commands while tolerating a limited number of node failures.

**Q57. What are the main roles in Raft?**  
Answer: The main roles are leader, follower, and candidate. The leader manages log replication, followers replicate the log, and candidates seek election.

**Q58. How does leader election work in Raft?**  
Answer: When a follower stops receiving heartbeats, it may become a candidate, start an election, and request votes. A candidate becomes leader after receiving a majority of votes in its term.

**Q59. What problem does Paxos solve?**  
Answer: Paxos is a family of consensus algorithms that allows distributed nodes to agree on a value despite certain failures.

**Q60. What is the difference between consensus and replication?**  
Answer: Replication copies data between nodes. Consensus coordinates agreement on decisions or operation order, often to make replicated state reliable.

**Q61. What is split-brain?**  
Answer: Split-brain occurs when multiple nodes or groups independently believe they are the active primary, potentially accepting conflicting writes.

**Q62. How can split-brain be mitigated?**  
Answer: Use quorum-based coordination, reliable leader election, fencing tokens, and mechanisms that prevent an old leader from continuing to write.

**Q63. What is a fencing token?**  
Answer: A fencing token is a monotonically increasing number issued with a lease or lock. A resource rejects operations carrying an older token.

## G. Clocks and Event Ordering

**Q64. What is clock skew?**  
Answer: Clock skew is the difference between the clock readings of different machines.

**Q65. Why can't we rely entirely on wall-clock timestamps to order distributed events?**  
Answer: Clocks can drift or be adjusted, and timestamps from different machines may not reflect the true causal order of events.

**Q66. What is a Lamport clock?**  
Answer: A Lamport clock is a logical counter that helps order events consistently with the happened-before relationship, though it cannot identify all concurrent events.

**Q67. What is a vector clock?**  
Answer: A vector clock tracks logical counters from multiple nodes and can help determine whether events are causally related or concurrent.

**Q68. What is the happened-before relationship?**  
Answer: It describes causal ordering: events in the same process, message sending, and the corresponding message receiving establish ordering relationships.

## H. Service Coordination and Architecture

**Q69. What is service discovery?**  
Answer: Service discovery lets services find the current network locations of other service instances dynamically.

**Q70. What is load balancing?**  
Answer: Load balancing distributes requests across multiple instances to improve resource utilization, throughput, and availability.

**Q71. What problems does ZooKeeper solve?**  
Answer: ZooKeeper provides coordination primitives that can support configuration management, naming, synchronization, and leader-election implementations.

**Q72. What is a distributed lock?**  
Answer: A distributed lock coordinates access to a shared resource across processes or machines. It needs careful handling of expiration, ownership, and stale lock holders.

**Q73. What is a lease?**  
Answer: A lease grants temporary ownership or permission that expires unless renewed, limiting how long a node can hold a resource.

**Q74. What is the gossip protocol?**  
Answer: Gossip is a decentralized protocol in which nodes periodically exchange information, gradually spreading membership or state updates through a cluster.

**Q75. What is the difference between a distributed lock and a database unique constraint?**  
Answer: A distributed lock coordinates work before it happens, while a unique constraint enforces data uniqueness at the database boundary. For duplicate business records, the database constraint is often the stronger final safeguard.

## Quick Review: Key Distinctions

| Concepts | Main difference |
|---|---|
| CAP vs. ACID consistency | Distributed read guarantees vs. database transaction invariants |
| Linearizability vs. eventual consistency | Real-time ordering guarantee vs. temporary replica divergence |
| Replication vs. sharding | Copy the same data vs. split different data |
| Retry vs. idempotency | Retry repeats an attempt; idempotency protects the business effect |
| 2PC vs. Saga | Coordinated atomic commit vs. local transactions with compensation |
| Consensus vs. replication | Agree on decisions/order vs. copy state |
| Lock vs. fencing token | Temporary coordination vs. rejecting stale lock holders |
| At-least-once vs. exactly-once effect | Possible duplicate delivery vs. deduplicated business outcome |

## Interview Tip

For scenario questions, explain the failure first, then the mechanism, then its trade-off. For example: a timeout does not prove that a remote operation failed; it only means the caller did not receive a response in time. Use idempotency to make retries safe, and use durable constraints or transactional state to protect business correctness.
