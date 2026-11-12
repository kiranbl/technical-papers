# Database Normalization

## Introduction

Normalization is the process of organizing data into tables to reduce repeated information. It helps us update data correctly and makes a database easier to maintain. For example, a college database may store students, courses and instructors. Keeping all their details in one table can cause unnecessary repetition.

## Common Normal Forms

- **First Normal Form (1NF):** Each cell should contain one value, not a list of values.
- **Second Normal Form (2NF):** The table must be in 1NF and non-key columns must depend on the whole key, not just part of a combined key.
- **Third Normal Form (3NF):** The table must be in 2NF and non-key columns should not depend on other non-key columns.

These are three common normal forms. Higher normal forms also exist.

## Example

A table that stores multiple courses in one cell is not in 1NF.

| student_id | name | courses |
|---|---|---|
| 1 | John | Python, SQL |
| 2 | Alice | Python |

We can organize this information into separate tables.

**Students**

| student_id | name |
|---|---|
| 1 | John |
| 2 | Alice |

**Courses**

| course_id | course | instructor_id |
|---|---|---|
| 101 | Python | 11 |
| 102 | SQL | 12 |

**Enrollments**

| student_id | course_id |
|---|---|
| 1 | 101 |
| 1 | 102 |
| 2 | 101 |

**Instructors**

| instructor_id | instructor_name |
|---|---|
| 11 | Priya |
| 12 | Ravi |

This design stores each student's and instructor's details in one place. IDs connect the related tables.

## Conclusion

Normalization reduces duplicate data and helps prevent mistakes when inserting, updating or deleting records. It makes database design clearer and easier to manage.

## References

- [IBM - What Is Database Normalization?](https://www.ibm.com/think/topics/database-normalization)
- [PostgreSQL - Constraints, Primary Keys and Foreign Keys](https://www.postgresql.org/docs/current/ddl-constraints.html)
