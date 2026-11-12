# Database Isolation Levels in PostgreSQL

## Introduction

Isolation levels control what a transaction can see when other transactions are running at the same time. They help a database handle multiple users without causing unexpected results. For example, one person might check a bank balance while another person updates it.

## Common Isolation Levels

- **Read Uncommitted:** In some databases, a transaction may read changes that have not been committed. PostgreSQL treats this level like Read Committed.
- **Read Committed:** A query reads committed data. Running the same query again may show a new value if another transaction has committed a change. This is PostgreSQL's default level.
- **Repeatable Read:** A transaction keeps a stable view of data, even if another transaction commits changes.
- **Serializable:** Transactions behave as if they ran one after another. PostgreSQL may cancel a conflicting transaction, which must then be retried.

## Example

Consider the following `accounts` table:

| id | name | balance |
|---|---|---|
| 1 | John | 1000 |
| 2 | Alice | 500 |

```sql
BEGIN TRANSACTION ISOLATION LEVEL REPEATABLE READ;

SELECT balance FROM accounts WHERE id = 1;

COMMIT;
```

With Repeatable Read, if another transaction updates John's balance after this transaction's first query, repeating the query in the same transaction still shows the earlier balance.

## Conclusion

Isolation levels decide how much change a transaction can see while other transactions are working. Choosing the correct level helps keep database operations reliable.

## References

- [PostgreSQL - Transaction Isolation](https://www.postgresql.org/docs/current/transaction-iso.html)
