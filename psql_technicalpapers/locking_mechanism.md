# Database Locking Mechanisms in PostgreSQL

## Introduction

Locking helps a database manage changes made by multiple users at the same time. For example, two people might try to book the last available seat. Locks help prevent conflicting updates to the same data.

## Common Locking Concepts

- **Row-level lock:** Protects a specific row from conflicting changes.
- **Table-level lock:** Controls certain operations on a whole table.
- **Shared lock:** Allows compatible shared access but blocks some conflicting operations.
- **Exclusive lock:** Prevents other transactions from performing conflicting operations.
- **Deadlock:** Happens when transactions wait for locks held by each other. PostgreSQL detects deadlocks and cancels one transaction.

## Example

Consider this `seats` table:

| seat_id | seat_number | available |
|---|---|---|
| 1 | A1 | TRUE |
| 2 | A2 | TRUE |

```sql
BEGIN;

SELECT * FROM seats
WHERE seat_id = 1
FOR UPDATE;

UPDATE seats
SET available = FALSE
WHERE seat_id = 1 AND available = TRUE
RETURNING seat_id;

COMMIT;
```

`FOR UPDATE` locks the selected row against conflicting updates until the transaction ends. The application should confirm that the seat was available and that the `UPDATE` returned a row before confirming the booking. A normal `SELECT` can still read the row because PostgreSQL uses MVCC.

## Conclusion

Locks help keep data correct when multiple users work at once. They should be used carefully because long transactions can make other transactions wait.

## References

- [PostgreSQL - Explicit Locking](https://www.postgresql.org/docs/current/explicit-locking.html)
- [PostgreSQL - Concurrency Control](https://www.postgresql.org/docs/current/mvcc.html)
- [PostgreSQL - SELECT and FOR UPDATE](https://www.postgresql.org/docs/current/sql-select.html)
