Q14. What is the difference between a process and a thread?

Answer: A process has its own memory space. Threads within the same process share memory and resources but have their own stacks.

Q15. What is the difference between synchronized and Lock?

Answer: Both provide synchronization. synchronized is built into Java, while Lock provides additional features such as timed acquisition and interruptible locking.

Q16. What does volatile do?

Answer: volatile ensures visibility of updates across threads and restricts certain instruction reorderings. It does not make compound operations atomic.

Q17. What is a deadlock?

Answer: A deadlock occurs when threads wait indefinitely for resources held by each other. We can reduce the risk by acquiring locks in a consistent order.

Q18. What is a ThreadPoolExecutor?

Answer: It manages a pool of reusable threads. It helps control concurrency, reduce thread creation overhead, and manage task queues.

Q19. What is the difference between Runnable and Callable?

Answer: Runnable does not return a result from its task. Callable can return a result and throw checked exceptions.

Q20. What is the purpose of CompletableFuture?

Answer: CompletableFuture supports asynchronous computation and lets us combine dependent tasks without blocking the main thread unnecessarily.