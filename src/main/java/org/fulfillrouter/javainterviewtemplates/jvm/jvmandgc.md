# JVM Interview Questions and Answers

**Java Backend Engineer | Short English Answers | Grouped by Topic**

## A. JVM Memory and Errors

### Q21. What are the main JVM memory areas?
**Answer:** The main areas include the heap, Java stacks, the method area, the program counter registers, and native method stacks. Objects are typically allocated on the heap.

### Q23. What is a memory leak in Java?
**Answer:** A memory leak happens when objects are no longer needed but remain reachable. They cannot be garbage-collected, so memory usage may continue to grow.

### Q24. What is the difference between `StackOverflowError` and `OutOfMemoryError`?
**Answer:** `StackOverflowError` often occurs because of excessively deep recursion. `OutOfMemoryError` occurs when the JVM cannot allocate memory as required.

### Q25. How would you investigate high memory usage in a Java application?
**Answer:** I would check JVM metrics and garbage collection logs, capture a heap dump if necessary, and use tools like Eclipse MAT to identify memory-heavy objects and possible leaks.

## B. Garbage Collection

### Q22. How does garbage collection work?
**Answer:** The JVM identifies objects that are no longer reachable and reclaims their memory. Different garbage collectors use different strategies to balance throughput and latency.

### Q77. What are GC roots?
**Answer:** GC roots are references from runtime locations such as active thread stacks, static fields, and JNI handles. The garbage collector treats objects reachable from these roots as live.

### Q78. What is the difference between the young and old generations?
**Answer:** Many collectors use a young generation for recently allocated objects and an old generation for objects that survive longer. Their collection strategies and frequencies differ, but the exact layout depends on the collector.

### Q79. What is G1 GC designed for?
**Answer:** G1 divides the heap into regions and aims to meet a configurable pause-time goal while collecting regions with substantial reclaimable space. The goal is a target, not a strict guarantee.

## C. Class Loading

### Q75. What are the main steps in Java class loading?
**Answer:** The lifecycle is loading, linking (verification, preparation, and resolution), and initialization. Resolution may be performed lazily when a symbolic reference is first used.

### Q76. What is parent delegation in class loading?
**Answer:** With parent delegation, a class loader asks its parent to load a class before trying itself. This helps avoid duplicate definitions of core classes, though frameworks and application servers may use specialized loading strategies.

## Quick Review

| Topic | Key point |
|---|---|
| Heap | Typically stores objects and arrays |
| Java stack | Holds per-thread frames for method calls and local variables |
| GC roots | Starting references used to determine reachability |
| Memory leak | Unneeded objects remain reachable |
| `StackOverflowError` | Often caused by excessive call-stack depth |
| `OutOfMemoryError` | The JVM cannot satisfy a memory allocation request |
| Class loading | Loading → linking → initialization |
| Parent delegation | Ask parent class loader before attempting local loading |
| G1 GC | Region-based collector with a pause-time target, not a guarantee |

