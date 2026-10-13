# Java Concurrency Interview Questions

## Group 1: Thread Basics and Thread Safety — Highest Priority

### Q1. What is the difference between a process and a thread?

**Answer:** A process has its own memory space. Threads within the same process share memory and resources but have their own stacks.

### Q2. What is the difference between `start()` and `run()`?

**Answer:** `start()` creates a new thread of execution and invokes `run()` on that thread. Calling `run()` directly executes the method on the current thread.

### Q3. What is a race condition, and how can it be prevented?

**Answer:** A race condition occurs when the result depends on the timing of concurrent operations. It can be prevented using synchronization, locks, atomic variables, or thread-safe data structures.

### Q4. What is the difference between `synchronized` and `Lock`?

**Answer:** Both provide synchronization. `synchronized` is built into Java, while `Lock` offers additional features such as timed and interruptible locking.

### Q5. What does `volatile` do?

**Answer:** `volatile` ensures visibility of updates across threads and restricts certain instruction reorderings. It does not make compound operations atomic.

### Q6. What is the difference between atomicity, visibility, and ordering?

**Answer:** Atomicity means an operation is indivisible. Visibility means updates are visible across threads. Ordering defines constraints on how operations may be reordered.

### Q7. What is the happens-before relationship?

**Answer:** Happens-before guarantees that certain actions performed by one thread are visible to another thread. It is established by rules involving synchronization, `volatile`, thread start, and thread join.

### Q8. What is a deadlock?

**Answer:** A deadlock occurs when threads wait indefinitely for resources held by each other. Acquiring locks in a consistent order helps prevent it.

## Group 2: Thread Coordination and Synchronization — High Priority

### Q9. What is the difference between `wait()`, `notify()`, and `notifyAll()`?

**Answer:** `wait()` releases the object's monitor and waits. `notify()` wakes one waiting thread, while `notifyAll()` wakes all waiting threads. The caller must own the same object's monitor.

### Q10. What is the difference between `sleep()` and `wait()`?

**Answer:** `sleep()` pauses the current thread without releasing its locks. `wait()` releases the object's monitor and waits until notified, interrupted, or timed out.

### Q11. What is the difference between `ReentrantLock` and `synchronized`?

**Answer:** Both provide mutual exclusion. `ReentrantLock` supports timed and interruptible acquisition and multiple conditions. Its lock must be released in a `finally` block.

### Q12. What is the difference between `CountDownLatch` and `CyclicBarrier`?

**Answer:** `CountDownLatch` lets threads wait until a count reaches zero and cannot be reset. `CyclicBarrier` lets a group of threads wait for one another and can be reused.

### Q13. What are common uses and risks of `ThreadLocal`?

**Answer:** `ThreadLocal` gives each thread its own value. In thread pools, call `remove()` when the value is no longer needed to prevent stale data and memory retention.

## Group 3: Thread Pools and Asynchronous Programming — High Priority

### Q14. What is a `ThreadPoolExecutor`?

**Answer:** It manages reusable threads to execute tasks, control concurrency, reduce thread creation overhead, and queue tasks.

### Q15. How does `ThreadPoolExecutor` work?

**Answer:** It first creates threads up to `corePoolSize`. After that, it queues tasks. If the queue is full, it creates threads up to `maximumPoolSize`. If both the pool and queue are full, it applies the rejection policy.

### Q16. What are the core parameters of `ThreadPoolExecutor`?

**Answer:** The main parameters are `corePoolSize`, `maximumPoolSize`, `keepAliveTime`, `workQueue`, `threadFactory`, and `handler`.

### Q17. What are the common thread pool rejection policies?

**Answer:** `AbortPolicy` throws an exception; `CallerRunsPolicy` executes the task in the submitting thread; `DiscardPolicy` silently drops the task; `DiscardOldestPolicy` drops the oldest queued task and retries submission.

### Q18. What is the difference between `Runnable` and `Callable`?

**Answer:** `Runnable` does not return a result, while `Callable` can return a result and throw checked exceptions.

### Q19. What is the difference between `Future` and `CompletableFuture`?

**Answer:** `Future` retrieves a result and supports cancellation but generally requires blocking to obtain the result. `CompletableFuture` supports callbacks, task composition, and asynchronous pipelines.

### Q20. What is the purpose of `CompletableFuture`?

**Answer:** `CompletableFuture` supports asynchronous computation and lets us combine dependent tasks using methods such as `thenApply()`, `thenCompose()`, and `thenCombine()`.

## Group 4: Concurrency Collections and Producer-Consumer — High Priority

### Q21. How does `ConcurrentHashMap` work?

**Answer:** In modern Java, `ConcurrentHashMap` uses CAS and synchronized operations on individual bins when necessary, allowing concurrent access without locking the entire map for every update.

### Q22. How do you implement the producer-consumer pattern using `BlockingQueue`?

**Answer:** Producers put tasks into a `BlockingQueue`, and consumers take tasks from it. The queue coordinates threads and can apply backpressure when bounded and full.

## Group 5: Advanced Concurrency — Medium to Lower Priority

### Q23. What is compare-and-set (CAS)?

**Answer:** CAS atomically updates a value only if it matches an expected value. It enables non-blocking algorithms but can suffer from contention and the ABA problem.

### Q24. What is the ABA problem?

**Answer:** The ABA problem occurs when a value changes from A to B and back to A, causing CAS to miss the intermediate change. Version stamps or `AtomicStampedReference` can help detect it.

## Runnable Examples

Run the examples:

`./gradlew runConcurrencyExamples`

Source file: `examples/ConcurrencyExamples.java`

