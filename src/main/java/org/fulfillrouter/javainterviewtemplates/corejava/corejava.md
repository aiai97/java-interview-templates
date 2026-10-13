# Core Java Interview Questions

## Group 1: Java Fundamentals — Highest Priority

### Q1. What is the difference between JDK, JRE, and JVM?

**Answer:** The JVM executes Java bytecode. The JRE provides the JVM and runtime libraries. The JDK includes development tools such as the compiler and debugger.

### Q2. Is Java pass-by-value or pass-by-reference?

**Answer:** Java is always pass-by-value. For objects, the value passed is a copy of the object reference, so a method can modify the object but cannot replace the caller's reference.

### Q3. What is the difference between `==` and `equals()`?

**Answer:** For objects, `==` compares references, while `equals()` compares logical equality if overridden. For primitive types, `==` compares values.

### Q4. What is the difference between `final`, `finally`, and `finalize()`?

**Answer:** `final` restricts reassignment, overriding, or inheritance depending on its use. `finally` defines a cleanup block. `finalize()` is deprecated and should not be used for resource cleanup.

### Q5. What is the difference between primitive types and wrapper classes?

**Answer:** Primitive types store values directly, while wrapper classes represent primitive values as objects. Wrappers are useful in generics and collections, but can introduce boxing overhead and null values.

## Group 2: Object-Oriented Programming — Highest Priority

### Q6. What are the four principles of OOP?

**Answer:** They are encapsulation, inheritance, polymorphism, and abstraction. They help organize code, manage complexity, and improve reusability.

### Q7. What is the difference between an interface and an abstract class?

**Answer:** An interface defines a contract, while an abstract class can provide shared state and implementation. A class can implement multiple interfaces but extend only one class.

### Q8. What is the difference between overloading and overriding?

**Answer:** Overloading uses the same method name with different parameter lists. Overriding lets a subclass provide its own implementation of an inherited method.

### Q9. What is the difference between compile-time and runtime polymorphism?

**Answer:** Overloading is resolved at compile time. Overridden instance methods are dynamically dispatched at runtime based on the actual object's class.

### Q10. What is the difference between encapsulation and abstraction?

**Answer:** Encapsulation hides internal state and controls access to it. Abstraction exposes essential behavior while hiding implementation details.

### Q11. What is the difference between inheritance and composition?

**Answer:** Inheritance models an “is-a” relationship. Composition models a “has-a” relationship and often provides more flexibility by delegating behavior to other objects.

## Group 3: Strings and Object Contracts — Highest Priority

### Q12. Why is `String` immutable in Java?

**Answer:** A `String` cannot change after creation. Immutability improves security, thread safety, and the reliability of string pooling and hash codes.

### Q13. What is the difference between `String`, `StringBuilder`, and `StringBuffer`?

**Answer:** `String` is immutable. `StringBuilder` is mutable and not thread-safe. `StringBuffer` is mutable and synchronizes its operations.

### Q14. What is the difference between `equals()` and `hashCode()`?

**Answer:** `equals()` checks logical equality, while `hashCode()` returns an integer used by hash-based collections. Equal objects must have the same hash code.

### Q15. Why should `equals()` and `hashCode()` be overridden together?

**Answer:** Hash-based collections use the hash code to locate candidates and `equals()` to check equality. Overriding only one can cause incorrect lookup behavior.

### Q16. What is the String Pool?

**Answer:** The String Pool stores canonical string instances so equivalent string literals can share objects. This reduces duplicate string objects and memory usage.

## Group 4: Collections Framework — Highest Priority

### Q17. What is the difference between `List`, `Set`, and `Map`?

**Answer:** A `List` allows duplicates and preserves positional order. A `Set` stores unique elements. A `Map` stores key-value pairs with unique keys.

### Q18. What is the difference between `ArrayList` and `LinkedList`?

**Answer:** `ArrayList` provides fast indexed access and efficient append operations. `LinkedList` supports efficient insertion or removal through an existing node position, but indexed access is slower.

### Q19. How does `HashMap` work internally?

**Answer:** `HashMap` uses a key's hash code to locate a bucket and `equals()` to distinguish keys. Collisions are handled using linked lists or tree bins under suitable conditions.

### Q20. What is the difference between `HashMap`, `LinkedHashMap`, and `TreeMap`?

**Answer:** `HashMap` does not guarantee iteration order. `LinkedHashMap` preserves encounter order, usually insertion order. `TreeMap` sorts keys according to their natural order or a comparator.

### Q21. What is the difference between `HashSet` and `TreeSet`?

**Answer:** `HashSet` stores unique elements without guaranteeing iteration order. `TreeSet` stores unique elements in sorted order.

### Q22. What is the difference between `Comparable` and `Comparator`?

**Answer:** `Comparable` defines a class's natural ordering through `compareTo()`. `Comparator` defines an external ordering through `compare()` and allows multiple sorting strategies.

## Group 5: Exception Handling and Resource Management — High Priority

### Q23. What is the difference between checked and unchecked exceptions?

**Answer:** Checked exceptions must be caught or declared. Unchecked exceptions are subclasses of `RuntimeException` or `Error` and do not have this compile-time requirement.

### Q24. What is the difference between `throw` and `throws`?

**Answer:** `throw` explicitly throws an exception. `throws` declares exceptions that a method may propagate to its caller.

### Q25. What is the purpose of `try-with-resources`?

**Answer:** It automatically closes resources that implement `AutoCloseable` when the block finishes, including when an exception occurs.

### Q26. What is the difference between `final`, `finally`, and `finalize()`?

**Answer:** `final` is a language modifier, `finally` is an exception-handling block, and `finalize()` is a deprecated cleanup mechanism that should be avoided.

## Group 6: Generics and Type System — Medium to High Priority

### Q27. What is type erasure in Java?

**Answer:** Java implements generics mainly through compile-time checks and type erasure. Most generic type parameters are erased from bytecode, which restricts certain operations on generic types.

### Q28. Why can't we use primitive types as generic type arguments?

**Answer:** Java generics require reference types. Use wrapper classes such as `Integer` instead of `int`.

### Q29. What is the difference between `? extends T` and `? super T`?

**Answer:** `? extends T` is useful when reading values as type `T`. `? super T` is useful when adding values of type `T`. This is commonly summarized as PECS: Producer Extends, Consumer Super.

## Group 7: Java 8+ Features — High Priority

### Q30. What is a functional interface?

**Answer:** A functional interface has exactly one abstract method and can be implemented with a lambda expression or method reference. Examples include `Runnable` and `Predicate`.

### Q31. What is a lambda expression?

**Answer:** A lambda expression provides a concise implementation of a functional interface, making behavior easier to pass as an argument.

### Q32. What is the Stream API?

**Answer:** The Stream API processes data through operations such as `filter`, `map`, and `collect`. Streams support declarative processing and can execute sequentially or in parallel.

### Q33. What is `Optional` used for?

**Answer:** `Optional` represents a value that may be absent and encourages explicit handling of that case. It is commonly used as a return type rather than as a replacement for every nullable field or parameter.

### Q34. What is a Java record?

**Answer:** A record is a concise way to define a data-oriented class. The compiler generates component accessors, a canonical constructor, `equals()`, `hashCode()`, and `toString()`.

## Runnable Examples

Run the examples:

`./gradlew runCoreJavaExamples`

Source file: `examples/CoreJavaExamples.java`
