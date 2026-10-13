# Spring Interview Questions: Business-Oriented Modifications

These questions focus on real backend engineering scenarios: adding features, changing business rules, integrating external services, and modifying existing Spring applications safely.

## A. High Priority — Business Logic and Design

### Q1. How would you add a new payment method to an existing payment system?

**Answer:** I would define a common `PaymentService` interface and implement the new payment method as a separate class. A strategy registry can select the implementation based on business data.

```java
public interface PaymentService {
    void pay();
}

@Service("alipay")
class AlipayService implements PaymentService {
    public void pay() {
        System.out.println("Paying with Alipay");
    }
}

@Service("wechat")
class WechatPayService implements PaymentService {
    public void pay() {
        System.out.println("Paying with WeChat Pay");
    }
}
```

### Q2. How would you add a new business rule without modifying existing code?

**Answer:** I would define an interface for the business rule and implement the new behavior separately. Dependency injection allows the application to use the new implementation with minimal changes to existing code.

### Q3. How would you select different implementations based on business requirements?

**Answer:** I would use `@Qualifier` to select a specific bean, `@Primary` to define a default bean, or a strategy registry when the implementation depends on runtime business data.

```java
public OrderService(
        @Qualifier("wechat") PaymentService paymentService) {
    this.paymentService = paymentService;
}
```

### Q4. How would you add validation before processing an order?

**Answer:** I would use Jakarta Bean Validation for request validation and put business-specific validation in the service layer.

```java
public class CreateOrderRequest {
    @NotNull
    private Long productId;
}
```

```java
@PostMapping("/orders")
public void create(@Valid @RequestBody CreateOrderRequest request) {
    orderService.create(request);
}
```

### Q5. How would you prevent duplicate order creation?

**Answer:** I would use an idempotency key or a unique business constraint to identify duplicate requests. The database should enforce uniqueness to handle concurrent requests safely.

### Q6. How would you make a business operation transactional?

**Answer:** I would use `@Transactional` on the service method that defines the transaction boundary. I would also verify rollback rules and ensure the method is invoked through Spring's transaction proxy.

```java
@Service
public class OrderService {
    @Transactional
    public void createOrder() {
        // Save order
        // Deduct inventory
    }
}
```

A database transaction does not automatically roll back external HTTP calls or messages.

## B. High Priority — Adding Features to Existing Systems

### Q7. How would you add caching to an existing service?

**Answer:** I would identify frequently accessed data, add caching at the service layer, and define expiration and invalidation rules. I would also consider stale data and cache consistency.

```java
@Cacheable(value = "products", key = "#productId")
public Product getProduct(Long productId) {
    return productRepository.findById(productId).orElseThrow();
}
```

### Q8. How would you add retry logic to a failing external API call?

**Answer:** I would use Spring Retry or a resilience library with bounded retries and backoff. I would retry transient failures and ensure that non-idempotent operations cannot execute twice unintentionally.

### Q9. How would you add asynchronous processing to a slow business operation?

**Answer:** I would move suitable work to an asynchronous worker or message queue. I would also define failure handling, retries, and monitoring.

```java
@Async
public void generateReport(Long reportId) {
    // Generate report
}
```

For durable, cross-process tasks, I would generally consider a message queue rather than relying only on `@Async`.

### Q10. How would you add auditing to existing business operations?

**Answer:** I would record the business identifier, operator, operation type, timestamp, and relevant changes. I could use an audit service or Spring AOP for cross-cutting logging.

### Q11. How would you add a new field to an existing API without breaking clients?

**Answer:** I would make the new field backward-compatible, preserve existing response fields, and define appropriate defaults. For breaking changes, I would consider API versioning.

### Q12. How would you add a new database operation to an existing Spring application?

**Answer:** I would add the repository or mapper method, implement the business logic in the service layer, and expose it through the controller if necessary. I would also add transaction handling and tests where appropriate.

## C. Medium–High Priority — Spring Framework Behavior

### Q13. Why might `@Transactional` not work after modifying a service method?

**Answer:** Common causes include self-invocation, calling a method outside the Spring proxy, incorrect transaction configuration, or an exception that does not trigger rollback.

### Q14. Why might `@Autowired` fail after adding a new implementation?

**Answer:** Spring may find multiple matching beans or no matching bean. I would check component scanning, bean types, `@Qualifier`, and `@Primary`.

### Q15. How would you add common logging without changing every service method?

**Answer:** I would use Spring AOP for cross-cutting concerns such as logging and execution-time measurement. Business-critical behavior should remain explicit in the service layer when that makes the logic easier to understand.

### Q16. How would you replace a third-party service implementation?

**Answer:** I would hide the external dependency behind an application-owned interface, implement a new adapter, and update the bean configuration. I would test compatibility and error handling before removing the old implementation.

## D. Medium–High Priority — Testing, Configuration, and Deployment

### Q17. How would you test a new Spring service feature?

**Answer:** I would write unit tests for business rules and integration tests for database interactions and Spring configuration. I would cover both successful and failure scenarios.

### Q18. How would you add environment-specific configuration?

**Answer:** I would use externalized configuration and Spring profiles to separate development, testing, and production settings. Secrets should be managed securely rather than hardcoded.

### Q19. How would you modify a service without affecting existing business flows?

**Answer:** I would keep the change small, preserve existing contracts, add regression tests, and deploy incrementally when possible. I would monitor errors and latency after release.

### Q20. How would you handle a failure in a multi-step business process?

**Answer:** I would identify the transaction boundary and failure points. For a single database transaction, I would use rollback. For distributed operations, I would consider idempotency, retries, compensating actions, and eventual consistency.

## Quick Review: Which Classes Would You Modify?

| Business requirement | Main classes or components |
|---|---|
| Add a payment or shipping method | Interface, implementation, strategy registry, service |
| Add order validation | Request DTO, validator, service |
| Prevent duplicate orders | Controller, service, database unique constraint |
| Add transaction management | Service, transaction configuration, database |
| Add caching | Service, cache configuration, invalidation logic |
| Retry external API calls | API adapter, retry configuration, exception handling |
| Process tasks asynchronously | Service, executor or message producer, consumer |
| Add auditing | AOP or audit service, database or logging system |
| Replace a third-party provider | Adapter, interface, configuration, tests |
| Prevent regressions | Unit tests, integration tests, regression tests |

**Recommended questions to master first:** Q1, Q3, Q5, Q6, Q7, Q8, Q13, Q19, and Q20. These cover Spring, Java design, database consistency, and practical backend engineering.
