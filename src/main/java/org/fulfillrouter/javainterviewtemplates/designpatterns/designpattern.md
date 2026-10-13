# Design Patterns Interview Questions and Answers

**Java Backend Engineer | Short English Answers | Grouped by Interview Frequency**

## A. High-Frequency Patterns

### 1. Strategy Pattern

**Q1. What is the Strategy pattern?**

Answer: The Strategy pattern defines interchangeable algorithms behind a common interface, allowing the application to select behavior without changing the caller.

**Q2. When would you use the Strategy pattern?**

Answer: Use it when multiple implementations solve the same problem, such as different payment methods, shipping providers, or pricing rules.

**Q3. How would you support multiple payment methods using the Strategy pattern?**

Answer: Define a `PaymentStrategy` interface, implement one class per payment method, and select the required strategy through dependency injection or a registry.

**Q4. What is the main benefit of the Strategy pattern?**

Answer: It separates business behavior into interchangeable implementations and makes adding new strategies easier without modifying existing algorithms.

**Q5. What is a potential drawback of the Strategy pattern?**

Answer: It can introduce many small classes and requires a clear way to select the appropriate strategy.

### 2. Factory Pattern

**Q6. What is the Factory pattern?**

Answer: A Factory encapsulates object creation so callers do not need to know the concrete class or construction details.

**Q7. When would you use a Factory?**

Answer: Use it when object creation depends on configuration, input, or business type, or when construction logic should be centralized.

**Q8. What is the difference between Factory and Strategy?**

Answer: A Factory decides which object to create. A Strategy defines interchangeable behavior after the object has been selected.

**Q9. What is the difference between Simple Factory and Factory Method?**

Answer: A Simple Factory usually selects and creates an implementation in one factory method. Factory Method lets subclasses determine which concrete product to create.

### 3. Singleton Pattern

**Q10. What is the Singleton pattern?**

Answer: Singleton restricts a class to one instance and provides a shared access point to it.

**Q11. How can you implement a thread-safe Singleton in Java?**

Answer: An enum Singleton is a simple robust option. The initialization-on-demand holder idiom is another common lazy-loading approach.

**Q12. Is a Spring singleton bean the same as the Singleton design pattern?**

Answer: Not exactly. A Spring singleton bean means one instance per bean definition per application context, while the classic Singleton pattern controls instance creation at the class level.

**Q13. What are the drawbacks of Singleton?**

Answer: It introduces global shared state, can hide dependencies, and may make testing harder. It should not be used merely to avoid creating objects.

### 4. Builder Pattern

**Q14. What is the Builder pattern?**

Answer: Builder constructs a complex object step by step, often improving readability when many optional parameters are involved.

**Q15. When would you use Builder in Java?**

Answer: Use it for objects with many optional fields, complex construction rules, or immutable configuration objects.

**Q16. What problem does Builder solve compared with constructors?**

Answer: It avoids long parameter lists and makes object creation more readable by naming each configured field.

### 5. Proxy Pattern

**Q17. What is the Proxy pattern?**

Answer: A Proxy controls access to another object while exposing a compatible interface.

**Q18. What are common uses of Proxy?**

Answer: Common uses include access control, lazy loading, remote calls, caching, and transaction or method interception.

**Q19. How does Spring AOP use proxies?**

Answer: Spring commonly creates JDK dynamic proxies or CGLIB proxies to intercept method calls and apply cross-cutting behavior such as transactions or logging.

**Q20. Why might `@Transactional` not work on a method call within the same class?**

Answer: In proxy-based Spring AOP, self-invocation bypasses the proxy, so the transaction interceptor is not triggered for that internal call.

**Q21. What is the difference between JDK dynamic proxies and CGLIB proxies?**

Answer: JDK dynamic proxies proxy interfaces. CGLIB creates a subclass to proxy a class, so final classes or final methods cannot be overridden for interception.

### 6. Adapter Pattern

**Q22. What is the Adapter pattern?**

Answer: An Adapter converts one interface into another interface that the client expects.

**Q23. When would you use an Adapter in a backend application?**

Answer: Use it to integrate a third-party payment, shipping, or messaging API behind an application-owned interface.

**Q24. Why is an Adapter useful when replacing a third-party provider?**

Answer: It isolates vendor-specific APIs from business logic, reducing the number of application components that must change.

### 7. Decorator Pattern

**Q25. What is the Decorator pattern?**

Answer: Decorator adds behavior to an object by wrapping it, without changing the original class.

**Q26. How is Decorator different from inheritance?**

Answer: Decorator composes behavior dynamically at runtime, while inheritance defines behavior through a class hierarchy.

**Q27. Give a Java backend example of Decorator.**

Answer: A service wrapper could add metrics, caching, or request logging around an existing service implementation.

### 8. Observer Pattern

**Q28. What is the Observer pattern?**

Answer: Observer allows multiple subscribers to be notified when a subject's state or event changes.

**Q29. When would you use Observer?**

Answer: Use it when one event should trigger multiple independent reactions, such as notifying users, updating analytics, and recording audit events after an order is placed.

**Q30. How is Observer related to event-driven architecture?**

Answer: Both use events to decouple producers from consumers. Distributed event-driven systems typically add a broker and must handle delivery failures and duplicate messages.

## B. Common Patterns in Frameworks and Business Code

### 9. Template Method Pattern

**Q31. What is the Template Method pattern?**

Answer: Template Method defines the overall algorithm in a base class while allowing subclasses to customize selected steps.

**Q32. When would you use Template Method?**

Answer: Use it when several workflows share the same sequence of steps but differ in a few specific operations.

**Q33. What is a drawback of Template Method?**

Answer: It relies on inheritance, which can make behavior harder to change or combine than composition.

### 10. Chain of Responsibility

**Q34. What is the Chain of Responsibility pattern?**

Answer: It passes a request through a sequence of handlers, where each handler can process the request or pass it onward.

**Q35. Where is Chain of Responsibility useful?**

Answer: It is useful for servlet filters, security checks, validation pipelines, request processing, and middleware.

**Q36. How is Chain of Responsibility different from Strategy?**

Answer: Strategy selects one interchangeable behavior. Chain of Responsibility runs or evaluates a sequence of handlers until processing stops or the chain finishes.

### 11. Facade Pattern

**Q37. What is the Facade pattern?**

Answer: Facade provides a simple interface over a complex subsystem.

**Q38. Give a backend example of Facade.**

Answer: An order facade could coordinate inventory, payment, and shipping services behind one application-facing operation.

### 12. Repository and Dependency Injection

**Q39. Is Repository a GoF design pattern?**

Answer: Repository is an architectural pattern, not one of the original 23 GoF patterns. It abstracts data access behind a collection-like interface.

**Q40. Is dependency injection a design pattern?**

Answer: Dependency injection is a design technique and an implementation of inversion of control that supplies dependencies from outside a class.

**Q41. What is the benefit of programming to an interface?**

Answer: It reduces coupling to concrete implementations and makes it easier to replace dependencies and test components independently.

## C. Other Frequently Asked Patterns

### 13. Abstract Factory

**Q42. What is the Abstract Factory pattern?**

Answer: Abstract Factory creates families of related objects without requiring the client to depend on their concrete classes.

**Q43. What is the difference between Factory Method and Abstract Factory?**

Answer: Factory Method delegates the creation of a product to a method or subclass. Abstract Factory provides an interface for creating a family of related products.

### 14. Command Pattern

**Q44. What is the Command pattern?**

Answer: Command encapsulates a request as an object, allowing requests to be queued, logged, retried, or executed later.

**Q45. Where is Command useful?**

Answer: It is useful for job queues, undoable operations, scheduled tasks, and separating request submission from execution.

### 15. State Pattern

**Q46. What is the State pattern?**

Answer: State represents state-dependent behavior in separate objects, allowing an object's behavior to change when its state changes.

**Q47. When would you use State in business systems?**

Answer: Use it when an order, payment, or workflow has distinct states with different allowed operations and transitions.

**Q48. What is the difference between State and Strategy?**

Answer: Strategy selects an algorithm, often based on configuration or input. State changes behavior based on the object's current state and transitions.

### 16. Iterator Pattern

**Q49. What is the Iterator pattern?**

Answer: Iterator provides a standard way to traverse a collection without exposing its internal representation.

**Q50. How does Java use the Iterator pattern?**

Answer: Java collections expose `Iterator` and `Iterable` so callers can traverse elements without depending on each collection's internal structure.

### 17. Composite Pattern

**Q51. What is the Composite pattern?**

Answer: Composite lets clients treat individual objects and groups of objects through the same interface.

**Q52. Where might Composite be used?**

Answer: It can represent tree structures such as file systems, organization hierarchies, or nested product categories.

### 18. Flyweight Pattern

**Q53. What is the Flyweight pattern?**

Answer: Flyweight reduces memory usage by sharing common immutable state across many logical objects.

**Q54. When is Flyweight useful?**

Answer: It is useful when a very large number of similar objects share data and object memory becomes expensive.

### 19. Prototype Pattern

**Q55. What is the Prototype pattern?**

Answer: Prototype creates new objects by copying existing instances rather than constructing them from scratch.

**Q56. What should you consider when cloning Java objects?**

Answer: Decide whether the copy should be shallow or deep, because a shallow copy still shares referenced mutable objects.

### 20. Mediator and Visitor

**Q57. What is the Mediator pattern?**

Answer: Mediator centralizes communication between related objects to reduce direct dependencies between them.

**Q58. What is the Visitor pattern?**

Answer: Visitor adds operations to a set of object types without putting each operation into those classes, typically using double dispatch.

## D. Design Principles Often Asked Alongside Patterns

**Q59. What is the SOLID principle?**

Answer: SOLID is a set of five object-oriented design principles intended to improve maintainability and extensibility: Single Responsibility, Open/Closed, Liskov Substitution, Interface Segregation, and Dependency Inversion.

**Q60. What is the Single Responsibility Principle?**

Answer: A class should have one cohesive responsibility and one primary reason to change.

**Q61. What is the Open/Closed Principle?**

Answer: Software entities should be open for extension but closed for modification, so new behavior can often be added without changing stable existing code.

**Q62. What is the Liskov Substitution Principle?**

Answer: A subtype should be usable wherever its base type is expected without breaking the program's expected behavior.

**Q63. What is the Interface Segregation Principle?**

Answer: Clients should not be forced to depend on methods they do not use. Prefer focused interfaces over large, general-purpose ones.

**Q64. What is the Dependency Inversion Principle?**

Answer: High-level policy should depend on abstractions rather than concrete low-level details; implementations should also depend on those abstractions.

**Q65. What is composition over inheritance?**

Answer: It means preferring object composition to reuse and combine behavior when that creates looser coupling than a rigid inheritance hierarchy.

**Q66. What is the difference between coupling and cohesion?**

Answer: Coupling measures how strongly components depend on each other. Cohesion measures how closely the responsibilities within one component belong together. Good designs generally aim for low coupling and high cohesion.

**Q67. What is the Open/Closed Principle's relationship to the Strategy pattern?**

Answer: Strategy allows new algorithms to be introduced as new implementations of an interface, often avoiding changes to the code that uses the strategy.

## E. Practical Design Questions

**Q68. How would you design a system that supports new payment providers with minimal changes?**

Answer: Define an application-owned payment interface, implement an adapter for each provider, and select the implementation through dependency injection or a registry. Keep provider-specific details outside core business logic.

**Q69. How would you add a new discount rule without creating many `if-else` statements?**

Answer: Model each discount algorithm as a Strategy implementation and select the applicable strategy through explicit business rules or a registry.

**Q70. How would you add logging and metrics without polluting business logic?**

Answer: Use decorators or framework-level interception such as Spring AOP where appropriate. Keep business-critical decisions explicit in the service layer.

**Q71. How would you make object creation easier to test?**

Answer: Move construction logic behind a factory or inject dependencies through constructors, allowing tests to supply controlled implementations.

**Q72. How do you decide whether to use a design pattern?**

Answer: Start with the concrete change or complexity you need to handle. Use a pattern when it reduces coupling or clarifies responsibilities; avoid adding abstraction without a real need.

**Q73. Can using too many design patterns be harmful?**

Answer: Yes. Unnecessary abstractions increase indirection and maintenance cost. The design should be as simple as possible while still handling the real requirements.

**Q74. How do you explain a design pattern in an interview?**

Answer: Explain the problem first, then the pattern's structure, how it changes the flow of control, and its trade-offs. Give a concrete example from the application.

## Quick Review: Pattern → Problem Solved

| Pattern | Main problem it solves |
|---|---|
| Strategy | Swap algorithms or business rules |
| Factory | Centralize or encapsulate object creation |
| Singleton | Share one controlled instance |
| Builder | Construct complex objects clearly |
| Proxy | Control or intercept access to an object |
| Adapter | Integrate an incompatible interface |
| Decorator | Add behavior through wrapping |
| Observer | Notify multiple subscribers about an event |
| Template Method | Reuse an algorithm skeleton with customizable steps |
| Chain of Responsibility | Process a request through handlers |
| Facade | Simplify access to a complex subsystem |
| Abstract Factory | Create families of related objects |
| Command | Encapsulate a request as an object |
| State | Vary behavior based on current state |
| Composite | Treat individual objects and groups uniformly |
| Flyweight | Share common state to reduce memory use |
| Repository | Abstract data access (architectural pattern) |
| Dependency Injection | Supply dependencies from outside a class |

