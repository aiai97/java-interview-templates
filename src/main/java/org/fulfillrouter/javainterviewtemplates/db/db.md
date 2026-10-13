# Database and SQL Interview Questions

## Group 1: SQL Fundamentals and Relational Database Concepts — Highest Priority

### Q1. What is the difference between SQL and NoSQL databases?

**Answer:** SQL databases typically use relational tables and structured schemas. NoSQL databases support models such as documents, key-value pairs, and wide-column storage. The choice depends on data relationships, consistency requirements, and access patterns.

### Q2. What is the difference between a primary key and a foreign key?

**Answer:** A primary key uniquely identifies a row. A foreign key references a key in another or the same table to enforce referential integrity.

### Q3. What are the different types of SQL joins?

**Answer:** `INNER JOIN` returns matching rows, `LEFT JOIN` preserves all left-side rows, `RIGHT JOIN` preserves all right-side rows, and `FULL OUTER JOIN` preserves rows from both sides.

### Q4. What is the difference between `WHERE` and `HAVING`?

**Answer:** `WHERE` filters rows before grouping. `HAVING` filters groups after aggregation.

### Q5. What is the difference between `DELETE`, `TRUNCATE`, and `DROP`?

**Answer:** `DELETE` removes selected rows, `TRUNCATE` removes all rows, and `DROP` removes the database object itself. Transactional behavior and other details depend on the database.

### Q6. What is the difference between `UNION` and `UNION ALL`?

**Answer:** `UNION` combines results and removes duplicates. `UNION ALL` preserves duplicates and is generally faster because it avoids duplicate elimination.

## Group 2: Indexes and Query Optimization — Highest Priority

### Q7. What is a database index?

**Answer:** An index speeds up data retrieval by reducing the amount of data the database needs to scan. However, it consumes storage and adds overhead to writes.

### Q8. What is the difference between clustered and non-clustered indexes?

**Answer:** A clustered index organizes table data according to its index key in databases that support this structure. A non-clustered index stores indexed keys and references to the corresponding rows. Implementations vary by database.

### Q9. What is a composite index, and why does column order matter?

**Answer:** A composite index covers multiple columns. Column order affects which queries can use it efficiently; in many B-tree indexes, the leftmost-prefix rule is important.

### Q10. How do you optimize a slow SQL query?

**Answer:** I examine the execution plan, check indexes and join conditions, reduce unnecessary data retrieval, and measure the impact of each change.

### Q11. What is a full table scan, and when does it happen?

**Answer:** A full table scan reads the table's rows to find matching data. It may occur when no suitable index exists or when scanning most of the table is cheaper than using an index.

### Q12. Why might a database not use an index?

**Answer:** The optimizer may estimate that a table scan is cheaper, or the query may use functions, incompatible data types, or predicates that prevent efficient index access.

### Q13. What is the difference between `OFFSET` pagination and keyset pagination?

**Answer:** `OFFSET` pagination skips a specified number of rows and can become expensive for large offsets. Keyset pagination uses the last-seen key to retrieve the next page efficiently when a suitable index exists.

## Group 3: Transactions and ACID — Highest Priority

### Q14. What is a database transaction?

**Answer:** A transaction groups database operations into a logical unit of work. It helps ensure that related changes succeed or fail according to transaction rules.

### Q15. What are the ACID properties?

**Answer:** ACID stands for Atomicity, Consistency, Isolation, and Durability. These properties help ensure reliable transaction processing.

### Q16. What are the common SQL transaction isolation levels?

**Answer:** The standard levels are Read Uncommitted, Read Committed, Repeatable Read, and Serializable. Higher isolation can prevent more anomalies but may reduce concurrency. Exact behavior varies by database.

### Q17. What are dirty reads, non-repeatable reads, and phantom reads?

**Answer:** A dirty read sees uncommitted data. A non-repeatable read returns a different value when the same row is read again. A phantom read occurs when repeating a query returns a different set of rows due to concurrent changes.

### Q18. What is the difference between `COMMIT` and `ROLLBACK`?

**Answer:** `COMMIT` makes a transaction's changes permanent according to the database's durability guarantees. `ROLLBACK` undoes uncommitted changes within the transaction.

## Group 4: Database Locking and Concurrency Control — High Priority

### Q19. What is a database deadlock?

**Answer:** A database deadlock occurs when transactions wait for locks held by each other. The database typically detects the deadlock and aborts one transaction.

### Q20. What is the difference between optimistic and pessimistic locking?

**Answer:** Optimistic locking detects conflicting updates, often using a version column. Pessimistic locking acquires locks before modification to prevent conflicting operations.

### Q21. What is MVCC?

**Answer:** Multi-Version Concurrency Control maintains multiple row versions so transactions can read consistent snapshots with less read-write blocking. Implementation details vary by database.

### Q22. What is the difference between optimistic locking and database isolation?

**Answer:** Optimistic locking detects conflicts on specific records, often through version checks. Isolation levels control which concurrent transaction effects a transaction can observe.

## Group 5: Data Modeling and Normalization — High Priority

### Q23. What is database normalization?

**Answer:** Normalization organizes data into related tables to reduce duplication and update anomalies. Denormalization may be useful when read performance justifies the trade-offs.

### Q24. What are the first three normal forms (1NF, 2NF, and 3NF)?

**Answer:** 1NF requires atomic column values. 2NF eliminates partial dependencies on part of a candidate key. 3NF eliminates inappropriate transitive dependencies between non-key attributes.

### Q25. What is the difference between normalization and denormalization?

**Answer:** Normalization reduces duplication and improves data integrity. Denormalization intentionally introduces redundancy to improve certain read or reporting workloads.

## Group 6: ORM and Application-Level Database Performance — High Priority for Java Backend

### Q26. What is the N+1 query problem?

**Answer:** It occurs when an application executes one query to fetch a collection and additional queries for individual records. It can be addressed with appropriate joins, batch fetching, or eager loading.

### Q27. What is connection pooling, and why is it needed?

**Answer:** Connection pooling reuses database connections instead of repeatedly creating and closing them. It reduces connection overhead and helps control database resource usage.

### Q28. What is the difference between lazy loading and eager loading?

**Answer:** Lazy loading retrieves related data when it is accessed. Eager loading retrieves it earlier, often with the initial query or a separate query. The right choice depends on access patterns and query costs.

## Group 7: Advanced Database Concepts — Medium Priority

### Q29. What is a covering index?

**Answer:** A covering index contains all the columns needed by a query, allowing the database to answer it from the index without fetching the corresponding table rows in supported execution plans.

### Q30. What is a database execution plan?

**Answer:** An execution plan describes how the database intends to execute a query, including scans, joins, and index access. Actual execution statistics help identify performance bottlenecks.

### Q31. What is the difference between B-tree and hash indexes?

**Answer:** B-tree indexes support equality and range queries and ordered access. Hash indexes are designed primarily for equality lookups, with capabilities and trade-offs depending on the database.

### Q32. What is database replication?

**Answer:** Replication copies data from one database server to another. It can improve availability and read scalability, but replication lag and consistency requirements must be considered.

## Runnable Practice

Practice SQL queries against a local PostgreSQL or MySQL database, especially:

- Joins and subqueries
- Finding the second-highest salary
- Grouping and aggregate queries
- Index selection and execution plans
- Transactions and concurrent updates
