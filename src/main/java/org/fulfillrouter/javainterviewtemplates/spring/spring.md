# Spring Framework and Spring Boot Interview Questions

## Group 1: Spring Core and Dependency Injection — Highest Priority

### Q1. What is the Spring Framework?

**Answer:** Spring is a Java framework that provides dependency injection, AOP, transaction management, and web application support.

### Q2. What is Inversion of Control (IoC)?

**Answer:** IoC means the framework controls object creation and lifecycle instead of application code managing them directly.

### Q3. What is Dependency Injection (DI)?

**Answer:** DI is a technique where an object's dependencies are provided by the container rather than created by the object itself.

### Q4. What is the difference between IoC and DI?

**Answer:** IoC is the general principle of transferring control to a framework. DI is a technique Spring uses to implement IoC.

### Q5. What is a Spring Bean?

**Answer:** A Spring Bean is an object managed by the Spring IoC container, which handles its creation, dependency injection, and lifecycle.

### Q6. What is the difference between constructor, setter, and field injection?

**Answer:** Constructor injection supplies dependencies during object creation, setter injection supplies them afterward, and field injection injects them directly into fields. Constructor injection is generally preferred for required dependencies.

### Q7. What is the difference between `@Component`, `@Service`, `@Repository`, and `@Controller`?

**Answer:** All identify Spring-managed components. `@Service` represents business logic, `@Repository` represents data access, and `@Controller` handles web requests.

### Q8. What is the difference between `@Component` and `@Bean`?

**Answer:** `@Component` marks a class for component scanning. `@Bean` marks a method whose returned object should be managed by Spring.

### Q9. What is the difference between `@Autowired`, `@Qualifier`, and `@Primary`?

**Answer:** `@Autowired` requests dependency injection. `@Qualifier` selects a specific bean, while `@Primary` defines the preferred bean when multiple candidates exist.

## Group 2: Bean Lifecycle and Configuration — High Priority

### Q10. What is the Spring Bean lifecycle?

**Answer:** Spring creates the bean, injects dependencies, runs initialization callbacks and post-processors, and then makes it available for use. Managed singleton beans receive destruction callbacks when the context shuts down.

### Q11. What is the difference between `BeanFactory` and `ApplicationContext`?

**Answer:** Both provide IoC container functionality. `ApplicationContext` adds features such as event publishing, internationalization, and convenient integration with application infrastructure.

### Q12. What is the difference between singleton and prototype bean scopes?

**Answer:** Singleton scope creates one shared instance per container. Prototype scope creates a new instance when requested from the container.

### Q13. What is a `BeanPostProcessor`?

**Answer:** A `BeanPostProcessor` can modify bean instances before and after initialization. Spring uses post-processors for features such as annotation processing and proxy creation.

### Q14. What is the difference between `BeanFactoryPostProcessor` and `BeanPostProcessor`?

**Answer:** `BeanFactoryPostProcessor` modifies bean definitions before regular bean creation. `BeanPostProcessor` works with bean instances during their lifecycle.

### Q15. What is the difference between `@Configuration` and `@Component`?

**Answer:** Both register Spring-managed classes. `@Configuration` specifically declares a configuration class, with enhanced inter-bean `@Bean` method behavior when proxying is enabled.

### Q16. What is a circular dependency in Spring?

**Answer:** A circular dependency occurs when beans depend on each other directly or indirectly. Constructor-based cycles generally fail to resolve, and the best solution is usually to redesign the dependency structure.

## Group 3: Spring AOP and Proxies — High Priority

### Q17. What is Spring AOP?

**Answer:** Spring AOP separates cross-cutting concerns such as logging, transactions, and security from business logic.

### Q18. What are Aspect, Advice, Pointcut, and Join Point?

**Answer:** An aspect groups cross-cutting logic. Advice defines what runs, a pointcut selects join points, and a join point is an execution point where advice may apply.

### Q19. What is the difference between JDK dynamic proxies and CGLIB proxies?

**Answer:** JDK dynamic proxies implement interfaces. CGLIB creates subclasses to intercept eligible methods. Final classes and final methods cannot be overridden by CGLIB proxies.

### Q20. Why does self-invocation bypass Spring AOP?

**Answer:** A call from one method to another within the same object bypasses the Spring proxy. Therefore, proxy-based advice such as `@Transactional` may not run on the internal call.

### Q21. What is the difference between Spring AOP and AspectJ?

**Answer:** Spring AOP primarily uses proxies to intercept method executions. AspectJ supports broader join points and can weave aspects into bytecode at compile time, post-compile time, or load time.

## Group 4: Spring Transactions — Highest Priority

### Q22. What does `@Transactional` do?

**Answer:** `@Transactional` declares transaction boundaries. Spring's transaction infrastructure typically uses AOP proxies to begin, commit, or roll back transactions.

### Q23. Why might `@Transactional` not work?

**Answer:** Common causes include self-invocation, non-proxied objects, inappropriate method visibility for the proxy mechanism, or incorrect transaction configuration.

### Q24. What is transaction propagation?

**Answer:** Propagation defines how a method's transaction interacts with an existing transaction, such as joining it with `REQUIRED` or starting an independent transaction with `REQUIRES_NEW`.

### Q25. What is the difference between `REQUIRED` and `REQUIRES_NEW`?

**Answer:** `REQUIRED` joins an existing transaction or creates one. `REQUIRES_NEW` suspends the current transaction and starts an independent one.

### Q26. When does Spring roll back a transaction by default?

**Answer:** By default, Spring rolls back on `RuntimeException` and `Error`, but not on checked exceptions. Rollback rules can be customized.

### Q27. What is the difference between programmatic and declarative transaction management?

**Answer:** Declarative management uses annotations or configuration to define transaction boundaries. Programmatic management explicitly controls transactions through APIs such as `TransactionTemplate`.

## Group 5: Spring Boot and Auto-Configuration — Highest Priority

### Q28. What is the difference between Spring and Spring Boot?

**Answer:** Spring provides the core framework and application infrastructure. Spring Boot simplifies application setup through auto-configuration, starter dependencies, and production-oriented features.

### Q29. What does `@SpringBootApplication` do?

**Answer:** It combines `@SpringBootConfiguration`, `@EnableAutoConfiguration`, and `@ComponentScan`.

### Q30. What is Spring Boot auto-configuration?

**Answer:** Auto-configuration conditionally configures beans based on the classpath, existing beans, and application properties.

### Q31. What are Spring Boot starters?

**Answer:** Starters are dependency bundles that simplify adding related capabilities, such as web development, database access, and testing.

### Q32. How do you configure different environments in Spring Boot?

**Answer:** Use externalized configuration and profiles, such as `application-dev.yml` and `application-prod.yml`, to separate environment-specific settings.

### Q33. What are `@Conditional` annotations?

**Answer:** They control whether configuration or beans are registered based on conditions such as classpath contents, existing beans, or property values.

## Group 6: Spring MVC and REST APIs — High Priority

### Q34. How does a request flow through Spring MVC?

**Answer:** The request reaches `DispatcherServlet`, which finds a handler, invokes the controller through the appropriate adapters, and processes the response through message converters or view rendering.

### Q35. What is the difference between `@Controller` and `@RestController`?

**Answer:** `@Controller` typically returns view names. `@RestController` combines `@Controller` and `@ResponseBody`, so methods return response data directly.

### Q36. What is the difference between `@RequestParam` and `@PathVariable`?

**Answer:** `@RequestParam` extracts query parameters or form parameters. `@PathVariable` extracts values from URI path segments.

### Q37. What is the purpose of `@ControllerAdvice`?

**Answer:** `@ControllerAdvice` provides shared controller behavior, commonly for centralized exception handling and response customization.

### Q38. How do you validate request data in Spring Boot?

**Answer:** Use Jakarta Bean Validation annotations such as `@NotNull` and `@Size`, typically combined with `@Valid` or `@Validated`.

## Group 7: Spring Ecosystem and Practical Backend Questions — Medium to High Priority

### Q39. What is the difference between `@Value` and `@ConfigurationProperties`?

**Answer:** `@Value` injects individual property values. `@ConfigurationProperties` binds groups of related properties to structured objects and supports type-safe configuration.

### Q40. What is Spring Data JPA?

**Answer:** Spring Data JPA simplifies database access by providing repository abstractions and generating common data-access operations.

### Q41. What is the N+1 query problem in Spring Data JPA?

**Answer:** It occurs when one query loads a collection and additional queries load related data for each item. Fetch joins, entity graphs