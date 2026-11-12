# Database Indexes in PostgreSQL

## Introduction

An index helps a database find information faster. It works like the index of a book, which helps us find a topic without reading every page. Indexes are useful when searching large tables, but they also take up storage space.

## Example Table: Employees

| id | name | email |
|---|---|---|
| 1 | John | john@gmail.com |
| 2 | Alice | alice@gmail.com |
| 3 | Bob | bob@gmail.com |

We can create an index on the `email` column:

```sql
CREATE INDEX idx_employee_email ON employees(email);
```

This index can make searches by email faster, especially when the table has many rows. PostgreSQL may still choose to scan the table when that is more efficient.

## Common Index Types

- **B-Tree:** Used for common searches and ranges. It is the default type.
- **Hash:** Used for equality searches.
- **GIN:** Useful for arrays and certain JSONB searches.
- **GiST:** Useful for specialized searches, including spatial data.
- **BRIN:** Useful for some very large tables with naturally ordered values.

These are only a few of PostgreSQL's index types.

## Conclusion

Indexes can improve query performance, but they also use storage and add work when data changes. We should create indexes where they are useful rather than indexing every column.

## References

- [PostgreSQL - Introduction to Indexes](https://www.postgresql.org/docs/current/indexes-intro.html)
- [PostgreSQL - Index Types](https://www.postgresql.org/docs/current/indexes-types.html)
- [PostgreSQL - CREATE INDEX](https://www.postgresql.org/docs/current/sql-createindex.html)
