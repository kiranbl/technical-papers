# SQL Joins in PostgreSQL

## Introduction

A JOIN is used to combine related information from two or more tables. For example, an employee's name can be stored in one table and the department name in another. We can connect these tables using a common column.

## Sample Tables

### Employees

| id | name | dept_id | manager_id |
|---|---|---|---|
| 1 | John | 101 | NULL |
| 2 | Alice | 102 | 1 |
| 3 | Bob | NULL | 1 |

### Departments

| dept_id | dept_name |
|---|---|
| 101 | IT |
| 102 | HR |
| 103 | Finance |

## Types of Joins

### 1. INNER JOIN

Returns only matching rows from both tables. John and Alice have matching departments.

```sql
SELECT e.name, d.dept_name
FROM employees e
INNER JOIN departments d ON e.dept_id = d.dept_id;
```

### 2. LEFT JOIN

Returns all employees, including Bob, who has no department.

```sql
SELECT e.name, d.dept_name
FROM employees e
LEFT JOIN departments d ON e.dept_id = d.dept_id;
```

### 3. RIGHT JOIN

Returns all departments, including Finance, which has no employees.

```sql
SELECT e.name, d.dept_name
FROM employees e
RIGHT JOIN departments d ON e.dept_id = d.dept_id;
```

### 4. FULL OUTER JOIN

Returns matching and unmatched rows from both tables. Bob and Finance are both included.

```sql
SELECT e.name, d.dept_name
FROM employees e
FULL OUTER JOIN departments d ON e.dept_id = d.dept_id;
```

### 5. CROSS JOIN

Returns every possible combination of rows from both tables. Three employees and three departments produce nine rows.

```sql
SELECT e.name, d.dept_name
FROM employees e
CROSS JOIN departments d;
```

### 6. SELF JOIN

Joins a table with itself. Here, we use it to find the manager of each employee. Alice and Bob both report to John.

```sql
SELECT e.name AS employee, m.name AS manager
FROM employees e
JOIN employees m ON e.manager_id = m.id;
```

## Conclusion

Joins help us get related information from different tables without storing everything in one place. We choose the type of JOIN based on which rows we want to display.

## References

- [PostgreSQL - Joins Between Tables](https://www.postgresql.org/docs/current/tutorial-join.html)
- [PostgreSQL - Table Expressions](https://www.postgresql.org/docs/current/queries-table-expressions.html)
