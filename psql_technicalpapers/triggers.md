# Database Triggers in PostgreSQL

## Introduction

A trigger is used to perform an action automatically when something changes in a database table. For example, we can display a message whenever a new student is added. We do not need to call the trigger ourselves because PostgreSQL runs it when the chosen event happens.

## Common Trigger Types

- **BEFORE:** Runs before an operation.
- **AFTER:** Runs after an operation.
- **INSERT:** Happens when a new row is added.
- **UPDATE:** Happens when an existing row changes.
- **DELETE:** Happens when a row is removed.

## Simple Example

Suppose we already have a `students` table:

| id | name |
|---|---|
| 1 | John |
| 2 | Alice |

We want PostgreSQL to show a message whenever someone adds a student.

**Step 1: Create the function.**

```sql
CREATE OR REPLACE FUNCTION student_message()
RETURNS TRIGGER AS $$
BEGIN
    RAISE NOTICE 'A new student was added!';
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

**Step 2: Connect the function to an INSERT event.**

```sql
CREATE TRIGGER after_student_insert
AFTER INSERT ON students
FOR EACH ROW
EXECUTE FUNCTION student_message();
```

**Step 3: Add a new student.**

```sql
INSERT INTO students VALUES (3, 'Ravi');
```

PostgreSQL automatically displays:

```text
NOTICE: A new student was added!
```

The notice is a message, not a row saved in the table. The student is added normally.

## Conclusion

Triggers help automate actions when data is inserted, updated or deleted. They can be useful for recording changes and checking data, but too many triggers can make a database harder to understand.

## References

- [PostgreSQL - Overview of Trigger Behavior](https://www.postgresql.org/docs/current/trigger-definition.html)
- [PostgreSQL - Trigger Functions](https://www.postgresql.org/docs/current/plpgsql-trigger.html)
- [PostgreSQL - CREATE TRIGGER](https://www.postgresql.org/docs/current/sql-createtrigger.html)
