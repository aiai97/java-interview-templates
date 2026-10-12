Q9. How does HashMap work?

Answer: HashMap uses a key's hash code to locate a bucket. It uses equals() to distinguish keys when necessary. Collisions are handled using linked lists or tree structures.

Q10. What is the difference between HashMap and ConcurrentHashMap?

Answer: HashMap is not thread-safe. ConcurrentHashMap supports concurrent access and is designed for better performance in multithreaded environments.

Q11. What is the difference between ArrayList and LinkedList?

Answer: ArrayList provides fast indexed access. LinkedList supports efficient insertion or removal when the relevant node position is already known, but indexed access is slower.

Q12. How does HashSet prevent duplicates?

Answer: HashSet uses a HashMap internally. It uses hash codes and equality checks to determine whether an element already exists.

Q13. Why should we override hashCode() when overriding equals()?

Answer: Equal objects must have the same hash code. Otherwise, hash-based collections such as HashMap may behave incorrectly.