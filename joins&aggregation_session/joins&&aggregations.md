# PostgreSQL — Joins and Aggregations

## 1. SQL Joins

A **JOIN** combines data from two tables using a related column or a matching condition. For example, we can combine employee names from one table with department names from another.

### Sample tables

**employees**

| emp_id | emp_name | dept_id | salary | manager_id |
|---|---|---|---:|---|
| 101 | Asha | 1 | 60000 | NULL |
| 102 | Ravi | 1 | 50000 | 101 |
| 103 | Meera | 2 | 45000 | 101 |
| 104 | Arjun | 3 | 40000 | 102 |
| 105 | Vikram | NULL | 35000 | 101 |
| 106 | Karan | 1 | 55000 | 101 |

**departments**

| dept_id | dept_name |
|---|---|
| 1 | Engineering |
| 2 | HR |
| 3 | Sales |
| 4 | Finance |

The tables are connected by `dept_id`. Vikram has no department and Finance has no employees; these examples help explain outer joins.

<details>
<summary>SQL to create and fill the sample tables</summary>

Run this in your demo database before trying the examples. It drops and recreates only these two sample tables, so any existing data in them will be deleted.

```sql
DROP TABLE IF EXISTS employees;
DROP TABLE IF EXISTS departments;

CREATE TABLE departments (
    dept_id INT PRIMARY KEY,
    dept_name VARCHAR(50)
);

CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(50),
    dept_id INT REFERENCES departments(dept_id),
    salary INT,
    manager_id INT REFERENCES employees(emp_id)
);

INSERT INTO departments VALUES
(1, 'Engineering'),
(2, 'HR'),
(3, 'Sales'),
(4, 'Finance');

INSERT INTO employees VALUES
(101, 'Asha', 1, 60000, NULL),
(102, 'Ravi', 1, 50000, 101),
(103, 'Meera', 2, 45000, 101),
(104, 'Arjun', 3, 40000, 102),
(105, 'Vikram', NULL, 35000, 101),
(106, 'Karan', 1, 55000, 101);
```

</details>

### INNER JOIN

Returns **only rows with matches in both tables**.

- Only rows matching the `ON` condition are returned.
- Vikram is excluded because her department is `NULL`.
- Use it when you need matching records from both tables.

![Animated INNER JOIN diagram](images/inner-join.gif)

```sql
SELECT e.emp_name, d.dept_name
FROM employees e
INNER JOIN departments d
ON e.dept_id = d.dept_id
ORDER BY e.emp_id;
```

**Result:** Five employees appear. Vikram is excluded because she has no matching department.

### LEFT JOIN

Returns **all rows from the left table** and matching rows from the right table. Missing values from the right table become `NULL`.

- Keeps every employee from the left table.
- Vikram appears with a `NULL` department.
- Useful when some employees may not have departments.

![Animated LEFT JOIN diagram](images/left-join.gif)

```sql
SELECT e.emp_name, d.dept_name
FROM employees e
LEFT JOIN departments d
ON e.dept_id = d.dept_id
ORDER BY e.emp_id;
```

**Result:** All six employees appear, including Vikram with `NULL` as the department name.

### RIGHT JOIN

Returns **all rows from the right table** and matching rows from the left table. Missing values from the left table become `NULL`.

- Keeps every department from the right table.
- Finance appears with a `NULL` employee.
- Swapping the tables and using `LEFT JOIN` gives equivalent rows.

![Animated RIGHT JOIN diagram](images/right-join.gif)

```sql
SELECT e.emp_name, d.dept_name
FROM employees e
RIGHT JOIN departments d
ON e.dept_id = d.dept_id
ORDER BY d.dept_id, e.emp_id;
```

**Result:** All departments appear, including Finance with a `NULL` employee name.

### FULL OUTER JOIN

Returns **matching and unmatched rows from both tables**.

- Keeps matched and unmatched rows from both tables.
- Both Vikram and Finance appear, with missing values as `NULL`.
- Useful for finding unmatched records.

![Animated FULL OUTER JOIN diagram](images/full-outer-join.gif)

```sql
SELECT e.emp_name, d.dept_name
FROM employees e
FULL OUTER JOIN departments d
ON e.dept_id = d.dept_id
ORDER BY e.emp_name NULLS LAST, d.dept_name;
```

**Result:** Vikram appears without a department and Finance appears without an employee. There are seven result rows.

> The Venn diagrams give a simplified picture of which rows are retained. Actual SQL joins can produce multiple rows for one matching key.

### SELF JOIN

A **SELF JOIN** joins a table to itself. It is useful when related records, such as employees and their managers, are stored in the same table. There is no separate `SELF JOIN` keyword; we use normal JOIN syntax with two aliases.

- Uses the same table twice with different aliases.
- Matches `manager_id` to the manager’s `emp_id`.
- Useful for employee–manager relationships.

```sql
SELECT
    e.emp_name AS employee,
    m.emp_name AS manager
FROM employees e
LEFT JOIN employees m
ON e.manager_id = m.emp_id
ORDER BY e.emp_id;
```

**Result:** Ravi's manager is Asha, Arjun's manager is Ravi, and Asha appears with a `NULL` manager because we used `LEFT JOIN`.

### CROSS JOIN

A **CROSS JOIN** creates every possible combination of rows from two tables. It does not need an `ON` condition.

- Pairs every employee with every department.
- 6 employees × 4 departments = 24 combinations.
- Useful for creating combinations; results can grow quickly.

```sql
SELECT e.emp_name, d.dept_name
FROM employees e
CROSS JOIN departments d
ORDER BY e.emp_id, d.dept_id
LIMIT 8;
```

**Result:** The first eight employee–department combinations are displayed. Without `LIMIT`, the two tables produce **6 × 4 = 24 rows**.

### NATURAL JOIN

A **NATURAL JOIN** automatically matches columns with the same names in both tables. By default, it uses inner-join behavior.

- Automatically matches columns with the same names.
- Here, it joins on `dept_id`, giving the same matches as INNER JOIN.
- Prefer explicit `ON` or `USING` because schema changes can affect results.

```sql
SELECT emp_name, dept_name
FROM employees
NATURAL JOIN departments
ORDER BY emp_id;
```

**Result:** Five employees with matching departments appear. Here, `dept_id` is the only column name shared by the tables, so this produces the same rows as our `INNER JOIN` example.

**Note:** `NATURAL JOIN` is supported by PostgreSQL, but it is usually better to use an explicit `ON` or `USING` condition in application code. Adding another identically named column to both tables can unexpectedly change a natural join's results.

---

## 2. Aggregate Functions

An **aggregate function** calculates one result from a set of rows, such as a count, total or average. `GROUP BY` and `HAVING` are explained separately below because they are SQL clauses, not functions.

### Common aggregate functions

| Function | Meaning |
|---|---|
| `COUNT()` | Counts rows or non-NULL values |
| `SUM()` | Finds the total |
| `AVG()` | Finds the average |
| `MIN()` | Finds the smallest value |
| `MAX()` | Finds the largest value |

```sql
SELECT
    COUNT(*) AS total_employees,
    SUM(salary) AS total_salary,
    AVG(salary) AS average_salary,
    MIN(salary) AS lowest_salary,
    MAX(salary) AS highest_salary
FROM employees;
```

**Result:** 6 employees, total salary 285000, average salary 47500, lowest salary 35000 and highest salary 60000.

### COUNT and DISTINCT

`COUNT(*)` counts all rows. `COUNT(column)` skips `NULL`. `COUNT(DISTINCT column)` counts unique non-NULL values.

```sql
SELECT
    COUNT(*) AS all_employees,
    COUNT(dept_id) AS assigned_employees,
    COUNT(DISTINCT dept_id) AS departments_with_employees
FROM employees;
```

**Result:** `6`, `5` and `3`.

### Other aggregate functions used by developers

PostgreSQL also provides aggregate functions useful for reports and backend applications. The following examples use the same `employees` table.

#### STRING_AGG() — combine text into a string

Combines non-NULL text values with a separator.

```sql
SELECT STRING_AGG(emp_name, ', ' ORDER BY emp_name) AS names
FROM employees
WHERE dept_id = 1;
```

**Result:** `Asha, Karan, Ravi`

#### ARRAY_AGG() — collect values in an array

Collects values into a PostgreSQL array.

```sql
SELECT ARRAY_AGG(emp_name ORDER BY emp_name) AS names
FROM employees
WHERE dept_id = 1;
```

**Result:** `{Asha,Karan,Ravi}`

#### JSON_AGG() — collect values in a JSON array

Creates a JSON array from multiple rows.

```sql
SELECT JSON_AGG(emp_name ORDER BY emp_name) AS names
FROM employees
WHERE dept_id = 1;
```

**Result:** `["Asha", "Karan", "Ravi"]`

#### JSONB_AGG() — collect values in a JSONB array

Works like `JSON_AGG()` but produces PostgreSQL's `jsonb` type.

```sql
SELECT JSONB_AGG(emp_name ORDER BY emp_name) AS names
FROM employees
WHERE dept_id = 1;
```

**Result:** `["Asha", "Karan", "Ravi"]` (type: `jsonb`)

#### JSONB_OBJECT_AGG() — create a JSONB object

Combines key-value pairs from rows into one JSONB object.

```sql
SELECT JSONB_OBJECT_AGG(emp_name, salary) AS salaries
FROM employees
WHERE dept_id = 1;
```

**Result (JSON key order may vary):**

```json
{"Asha": 60000, "Ravi": 50000, "Karan": 55000}
```

#### BOOL_AND() — check whether all values are true

Returns `TRUE` when every non-NULL input condition is true.

```sql
SELECT BOOL_AND(salary >= 40000) AS all_earn_40k
FROM employees;
```

**Result:** `false` because Vikram earns 35000.

#### BOOL_OR() — check whether any value is true

Returns `TRUE` when at least one non-NULL input condition is true.

```sql
SELECT BOOL_OR(salary > 55000) AS anyone_above_55k
FROM employees;
```

**Result:** `true` because Asha earns 60000.

Other specialized aggregates include statistical functions and percentile calculations. Refer to the [official list of PostgreSQL aggregate functions](https://www.postgresql.org/docs/current/functions-aggregate.html) for more details.

---

## 3. WHERE, GROUP BY and HAVING (SQL Clauses)

`WHERE`, `GROUP BY` and `HAVING` are **SQL clauses, not aggregate functions**. We often use them with aggregate functions such as `COUNT()`, `SUM()` and `AVG()` to calculate results for specific groups.

| Clause | Simple meaning | What it does |
|---|---|---|
| `WHERE` | **Filter individual rows** | Selects rows that meet a condition before grouping |
| `GROUP BY` | **Put similar rows into groups** | Creates one group for each distinct value or combination of values |
| `HAVING` | **Filter groups** | Keeps only groups that meet a condition, often using an aggregate |

### WHERE

**Definition:** `WHERE` selects only the rows that satisfy a condition. It filters individual records *before* any grouping happens.

**Example — find employees earning more than 50000:**

```sql
SELECT emp_name, salary
FROM employees
WHERE salary > 50000
ORDER BY emp_id;
```

**Result:** Asha (60000) and Karan (55000).

### GROUP BY

**Definition:** `GROUP BY` puts rows that have the same value into a group. We can then use an aggregate function to calculate a separate result for each group.

**Example — count employees in each assigned department:**

```sql
SELECT dept_id, COUNT(*) AS total_employees
FROM employees
WHERE dept_id IS NOT NULL
GROUP BY dept_id
ORDER BY dept_id;
```

| dept_id | total_employees |
|---:|---:|
| 1 | 3 |
| 2 | 1 |
| 3 | 1 |

**Explanation:** All employees with department ID 1 are counted together, then the same is done for departments 2 and 3.

### HAVING

**Definition:** `HAVING` filters the *groups* after aggregation. We use it when we need conditions such as “departments with more than one employee.”

**Example — show only departments with more than one employee:**

```sql
SELECT dept_id, COUNT(*) AS total_employees
FROM employees
WHERE dept_id IS NOT NULL
GROUP BY dept_id
HAVING COUNT(*) > 1;
```

| dept_id | total_employees |
|---:|---:|
| 1 | 3 |

**Explanation:** `GROUP BY` first forms the department groups. `COUNT(*)` calculates each group's size. `HAVING` displays only the groups where that count is greater than 1.

### WHERE vs GROUP BY vs HAVING in one query

```sql
SELECT dept_id, COUNT(*) AS total_employees
FROM employees
WHERE salary >= 40000 AND dept_id IS NOT NULL
GROUP BY dept_id
HAVING COUNT(*) > 1;
```

**Result:** Department 1 with 3 employees.

- **`WHERE`** keeps employees earning at least 40000 who have a department.
- **`GROUP BY`** groups those employees by department ID.
- **`COUNT(*)`** counts employees in each group.
- **`HAVING`** returns only groups containing more than one employee.

**Remember:** `WHERE` filters **rows**, `GROUP BY` makes **groups**, and `HAVING` filters **groups**. They work with aggregate functions, but are not aggregate functions themselves.

### FILTER (aggregate-specific condition)

`FILTER` applies a condition to one aggregate calculation, without removing rows from the inputs to other aggregate calculations in the same query.

```sql
SELECT
    COUNT(*) AS total_employees,
    COUNT(*) FILTER (WHERE salary > 50000) AS high_earners
FROM employees;
```

**Result:** `6` total employees and `2` employees earning more than 50000.

---

## 4. Combining JOINs and Aggregations

JOINs and aggregate functions can be used together. For example, we can count employees in each department, including departments with no employees.

```sql
SELECT
    d.dept_name,
    COUNT(e.emp_id) AS total_employees
FROM departments d
LEFT JOIN employees e
ON d.dept_id = e.dept_id
GROUP BY d.dept_id, d.dept_name
ORDER BY d.dept_id;
```

| dept_name | total_employees |
|---|---:|
| Engineering | 3 |
| HR | 1 |
| Sales | 1 |
| Finance | 0 |

`LEFT JOIN` keeps all departments, `GROUP BY` creates one group for each department and `COUNT(e.emp_id)` counts the matching employees. Since Finance has no matching employee ID, its count is `0`.

---

## 5. References

Official PostgreSQL documentation:

1. [Joins Between Tables — PostgreSQL Tutorial](https://www.postgresql.org/docs/current/tutorial-join.html)
2. [Joined Tables — PostgreSQL Documentation](https://www.postgresql.org/docs/current/queries-table-expressions.html#QUERIES-JOIN)
3. [Aggregate Functions — PostgreSQL Tutorial](https://www.postgresql.org/docs/current/tutorial-agg.html)
4. [Built-in Aggregate Functions — Full List](https://www.postgresql.org/docs/current/functions-aggregate.html)
5. [Aggregate Expressions — DISTINCT and FILTER](https://www.postgresql.org/docs/current/sql-expressions.html#SYNTAX-AGGREGATES)
6. [GROUP BY and HAVING](https://www.postgresql.org/docs/current/queries-table-expressions.html#QUERIES-GROUP)
