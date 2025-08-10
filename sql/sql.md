# SQL for Testers — Quick Reference

PURPOSE: Provide common SQL queries and patterns QA engineers use for validating backend state,
performing simple data setup/teardown, and checking data integrity.

## Basic SELECT
```sql
-- fetch user by id
SELECT id, username, email, created_at
FROM users
WHERE id = 123;
```

## WHERE patterns
```sql
-- partial match
SELECT * FROM orders WHERE order_number LIKE '2025-%';

-- range
SELECT * FROM transactions WHERE amount BETWEEN 100 AND 500;
```

## JOINs
```sql
SELECT o.id, o.order_number, u.username
FROM orders o
JOIN users u ON o.user_id = u.id
WHERE o.status = 'COMPLETED';
```

## INSERT / DELETE / UPDATE (use carefully)
```sql
INSERT INTO test_users (username, email, created_at)
VALUES ('qa_user_1','qa@example.com', NOW());

UPDATE users SET status = 'inactive' WHERE last_login < '2024-01-01';

DELETE FROM temp_sessions WHERE created_at < NOW() - INTERVAL '7 days';
```

## Test DB best practices
- Use a dedicated test database or schema
- Wrap changes in transactions and rollback when possible
- Use fixtures or migrations to create predictable data states
- Avoid destructive queries on shared environments

## JDBC example (Java) for validation
```java
String url = "jdbc:postgresql://localhost:5432/testdb";
Connection conn = DriverManager.getConnection(url, "user", "pass");
Statement stmt = conn.createStatement();
ResultSet rs = stmt.executeQuery("SELECT count(*) FROM users WHERE email='qa@example.com'");
if (rs.next()) {
    int count = rs.getInt(1);
    // assert count == 1
}
rs.close();
stmt.close();
conn.close();
```
