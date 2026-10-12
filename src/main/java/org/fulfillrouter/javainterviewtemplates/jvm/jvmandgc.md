Q21. What are the main JVM memory areas?

Answer: The main areas include the heap, Java stacks, the method area, the program counter registers, and native method stacks. Objects are typically allocated on the heap.

Q22. How does garbage collection work?

Answer: The JVM identifies objects that are no longer reachable and reclaims their memory. Different garbage collectors use different strategies to balance throughput and latency.

Q23. What is a memory leak in Java?

Answer: A memory leak happens when objects are no longer needed but remain reachable. They cannot be garbage-collected, so memory usage may continue to grow.

Q24. What is the difference between StackOverflowError and OutOfMemoryError?

Answer: StackOverflowError often occurs because of excessively deep recursion. OutOfMemoryError occurs when the JVM cannot allocate memory as required.

Q25. How would you investigate high memory usage in a Java application?

Answer: I would check JVM metrics and garbage collection logs, capture a heap dump if necessary, and use tools like Eclipse MAT to identify memory-heavy objects and possible leaks.