Q26. What is Dependency Injection?

Answer: Dependency Injection means an object receives its dependencies from an external container instead of creating them itself. It reduces coupling and improves testability.

Q27. What is IoC in Spring?

Answer: Inversion of Control means the framework manages object creation and their lifecycle. Spring implements this mainly through its IoC container.

Q28. What is a Spring Bean?

Answer: A Spring Bean is an object managed by the Spring container. Spring can create it, inject its dependencies, and manage its lifecycle.

Q29. What is the difference between @Component, @Service, and @Repository?

Answer: All three can register Spring-managed beans. @Component is generic, @Service marks business logic, and @Repository marks data-access components.

Q30. What is AOP?

Answer: Aspect-Oriented Programming separates cross-cutting concerns from business logic. Common examples include logging, transaction management, and security.

Q31. How does @Transactional work?

Answer: Spring typically uses AOP proxies to manage transactions around method calls. The transaction is committed on success and rolled back according to the configured rollback rules.

Q32. Why might @Transactional not work?

Answer: Common reasons include self-invocation bypassing the proxy, incorrect transaction configuration, and exceptions that do not trigger rollback under the configured rules.

Q33. What is the difference between Spring and Spring Boot?

Answer: Spring provides the core application framework. Spring Boot simplifies configuration and deployment through auto-configuration, starter dependencies, and embedded servers.

Q34. What is Spring Boot auto-configuration?

Answer: Auto-configuration configures beans based on the classpath, existing beans, and application properties. It reduces manual configuration while allowing customization.

Q35. What is the difference between BeanFactory and ApplicationContext?

Answer: BeanFactory provides basic dependency injection and bean management. ApplicationContext adds features such as events, internationalization, and integration with other Spring facilities.