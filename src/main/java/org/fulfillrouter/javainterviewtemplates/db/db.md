Q36. What is a database index?

Answer: An index speeds up data retrieval by reducing the amount of data the database needs to scan. However, it consumes storage and adds overhead to writes.

Q37. What is the difference between clustered and non-clustered indexes?

Answer: A clustered index determines how table rows are organized in the index structure. A non-clustered index stores indexed keys and references to the corresponding rows. The exact implementation depends on the database.

Q38. What are the ACID properties?

Answer: ACID stands for Atomicity, Consistency, Isolation, and Durability. These properties help ensure reliable transaction processing.

Q39. What is a database transaction?

Answer: A transaction groups database operations into a logical unit of work. It helps ensure that related changes succeed or fail according to the transaction rules.

Q40. What is a database deadlock?

Answer: A database deadlock occurs when transactions wait for locks held by each other. The database typically detects the deadlock and aborts one transaction.

Q41. How do you optimize a slow SQL query?

Answer: I would examine the execution plan, check indexes and join conditions, reduce unnecessary data retrieval, and measure the impact of each change.

Q42. What is the N+1 query problem?

Answer: It occurs when an application executes one query to fetch a collection and then additional queries for individual records. We can address it with appropriate joins, batch fetching, or eager loading.