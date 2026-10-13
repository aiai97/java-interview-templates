# Java Collections Interview Questions & Answers
**Java Backend Engineer | Short English Answers | Grouped by Interview Priority**

> Priority levels are practical preparation estimates, not official interview-frequency statistics. Actual questions vary by company and role.

## S Tier — Highest Priority

### Q1. How does HashMap work?
HashMap uses a key's hash code to locate a bucket and `equals()` to compare keys. It handles collisions using linked lists or tree structures.

### Q2. What is the difference between HashMap and ConcurrentHashMap?
HashMap is not thread-safe. ConcurrentHashMap supports concurrent access with thread-safe operations.

### Q3. Why should we override equals() and hashCode() together?
Equal objects must have the same hash code. Otherwise, hash-based collections may not work correctly.

### Q4. How does HashSet prevent duplicates?
HashSet uses a HashMap internally and relies on `hashCode()` and `equals()` to identify duplicate elements.

### Q5. What is the difference between ArrayList and LinkedList?
ArrayList provides fast indexed access. LinkedList supports efficient insertion and removal when the target node is already reached, but indexed access is slower.

### Q6. What is the difference between HashMap and TreeMap?
HashMap does not guarantee key order. TreeMap sorts keys by their natural ordering or a supplied Comparator.

### Q7. What is the time complexity of HashMap operations?
Get and put operations are O(1) on average. In the worst case, they can take O(n), although tree bins can improve collision-heavy lookups.

### Q8. How does ConcurrentHashMap achieve thread safety?
In modern Java, ConcurrentHashMap uses CAS and synchronized locking for certain bucket operations, allowing multiple threads to access the map concurrently.

## A Tier — High Priority

### Q9. How does ArrayList grow when it runs out of capacity?
ArrayList creates a larger backing array and copies the existing elements into it. Resizing takes O(n) time.

### Q10. What happens when two HashMap keys have the same hash code?
A hash collision occurs. HashMap uses `equals()` to distinguish the keys within the same bucket.

### Q11. Can HashMap contain null keys and values?
Yes. HashMap allows one null key and multiple null values.

### Q12. Does HashMap guarantee iteration order?
No. HashMap does not guarantee iteration order.

### Q13. What is a fail-fast iterator?
A fail-fast iterator may throw ConcurrentModificationException when it detects structural modifications outside the iterator. It is a bug-detection mechanism, not a thread-safety guarantee.

### Q14. How can you safely remove elements while iterating?
Use `Iterator.remove()` or `removeIf()` when appropriate. Avoid directly modifying the collection during iteration.

### Q15. When would you use a List, Set, or Map?
Use List for ordered elements, Set for unique elements, and Map for key-value pairs.

### Q16. What is the difference between Comparable and Comparator?
Comparable defines a class's natural ordering through `compareTo()`. Comparator defines an external or custom ordering through `compare()`.

### Q17. What is the difference between HashSet and TreeSet?
HashSet stores unique elements without guaranteeing sorted order. TreeSet stores unique elements in sorted order.

### Q18. What is the difference between ConcurrentHashMap and Hashtable?
Both are thread-safe. ConcurrentHashMap generally provides better concurrency, while Hashtable synchronizes its methods.

## B Tier — Medium Priority

### Q19. How does HashMap handle collisions internally?
HashMap stores colliding entries in the same bucket, using a linked list or a red-black tree when treeification conditions are met.

### Q20. What happens during HashMap resizing?
HashMap allocates a larger table and redistributes existing entries into the new table. Resizing is triggered when the size exceeds the threshold.

### Q21. What happens if a mutable object is used as a HashMap key?
If the key's hash code or equality changes after insertion, the entry may become difficult to retrieve. Immutable keys are generally safer.

### Q22. How does PriorityQueue order its elements?
PriorityQueue uses a heap to keep the highest-priority element at the head. By default, the smallest element comes first.

### Q23. What is the difference between Iterator and ListIterator?
Iterator supports forward traversal and element removal. ListIterator also supports backward traversal, insertion, and replacement for lists.

### Q24. What is the difference between synchronizedMap and ConcurrentHashMap?
Collections.synchronizedMap synchronizes access through a common wrapper lock. ConcurrentHashMap allows more concurrent operations.

### Q25. What is CopyOnWriteArrayList, and when would you use it?
CopyOnWriteArrayList creates a copy of its underlying array for write operations. It is useful when reads are frequent and writes are rare.

### Q26. What is BlockingQueue, and where is it used?
BlockingQueue is a thread-safe queue that can block producers when full and consumers when empty. It is commonly used in producer-consumer systems.

### Q27. How can you implement an LRU cache?
Use a HashMap for fast lookup and a doubly linked list to track usage order. Alternatively, use LinkedHashMap with access ordering.

## C Tier — Lower Priority / Source-Level Details

### Q28. Why does HashMap use a power-of-two capacity?
A power-of-two capacity allows efficient bucket indexing using a bitwise operation instead of modulo.

### Q29. How does LinkedHashMap maintain insertion order?
LinkedHashMap maintains a doubly linked list connecting its entries in iteration order.

### Q30. How does LinkedHashMap implement access-order iteration?
In access-order mode, LinkedHashMap moves accessed entries toward the end of its linked list.

### Q31. How does TreeMap maintain sorted keys?
TreeMap uses a red-black tree to maintain sorted keys and typically provides O(log n) lookup, insertion, and deletion.

### Q32. How does PriorityQueue implement a heap?
It uses an array-backed binary heap. Insertion moves elements upward, while removal moves elements downward to maintain the heap property.

### Q33. What is the difference between Arrays.asList() and ArrayList?
Arrays.asList() returns a fixed-size list backed by an array. ArrayList supports adding and removing elements.

### Q34. What is the difference between an unmodifiable collection and a synchronized collection?
An unmodifiable collection prevents modification through its exposed interface. A synchronized collection coordinates access between threads, but compound operations and iteration may still require external synchronization.

---

## Recommended Study Order

1. **S Tier (Q1–Q8):** Learn the core data structures and concurrency basics.
2. **A Tier (Q9–Q18):** Practise comparisons, complexity, and common pitfalls.
3. **B Tier (Q19–Q27):** Prepare deeper explanations and business use cases.
4. **C Tier (Q28–Q34):** Review implementation details after the fundamentals.

**Interview tip:** Memorize the direct answer first, then prepare one example and one follow-up explanation for each high-priority question.
