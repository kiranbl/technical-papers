# Database Transactions in PostgreSQL

## Introduction

A transaction is a group of database operations handled as one task. It helps prevent incomplete changes. For example, when we transfer money from one bank account to another, the money should be deducted from one account and added to the other. Both steps must succeed before the transfer is saved.

## Common Transaction Commands

- **BEGIN:** Starts a transaction.
- **COMMIT:** Saves the transaction's changes.
- **ROLLBACK:** Cancels all uncommitted changes in the transaction.
- **SAVEPOINT:** Marks a point inside a transaction.
- **ROLLBACK TO SAVEPOINT:** Cancels changes made after that point.
- **RELEASE SAVEPOINT:** Removes a savepoint without cancelling its changes.

## Example

Consider this `accounts` table:

| id | name | balance |
|---|---|---|
| 1 | John | 1000 |
| 2 | Alice | 500 |

The following transaction transfers 200 from John to Alice:

```sql
BEGIN;

UPDATE accounts SET balance = balance - 200 WHERE id = 1;
UPDATE accounts SET balance = balance + 200 WHERE id = 2;

COMMIT;
```

If we want to cancel the transaction before saving it, we can use `ROLLBACK` instead of `COMMIT`. A savepoint lets us undo only part of a transaction. In a real application, we must also check that both accounts exist and the sender has enough balance before committing.

## Conclusion

Transactions keep related database changes together. They are useful in banking, shopping and booking applications where incomplete updates can cause problems.

## References

- [PostgreSQL - Transactions](https://www.postgresql.org/docs/current/tutorial-transactions.html)
- [PostgreSQL - SAVEPOINT](https://www.postgresql.org/docs/current/sql-savepoint.html)
- [PostgreSQL - BEGIN](https://www.postgresql.org/docs/current/sql-begin.html)
