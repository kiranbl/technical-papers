# Aggregations and Filters in PostgreSQL

## Introduction

Aggregate functions calculate a result from multiple rows. They help us find totals, averages and counts. PostgreSQL has many aggregate functions. The following are just a few of the most commonly used ones.

## Sample Table: sales

| id | category | amount |
|---|---|---|
| 1 | Electronics | 1000 |
| 2 | Electronics | 100 |
| 3 | Furniture | 400 |
| 4 | Furniture | 300 |
| 5 | Electronics | 200 |

## Common Aggregate Functions

- **COUNT():** Counts rows or non-NULL values.
- **SUM():** Adds values.
- **AVG():** Calculates the average.
- **MIN():** Finds the smallest value.
- **MAX():** Finds the largest value.
- **STRING_AGG():** Combines text values into one string.
- **ARRAY_AGG():** Collects values into an array.

These are only a few examples. PostgreSQL supports many more aggregate functions.

## Filters and Grouping

- **WHERE:** Filters rows before grouping.
- **GROUP BY:** Groups rows with the same value.
- **HAVING:** Filters groups after aggregation.
- **FILTER:** Applies a condition to one aggregate function.

These clauses help with aggregation, but they are not themselves aggregate functions.

## Example

```sql
SELECT category, SUM(amount) AS total
FROM sales
GROUP BY category
HAVING SUM(amount) > 1000;
```

This query adds the sales amounts for each category and shows only totals above 1000. The result is **Electronics — 1300**.

## Conclusion

Aggregations summarize data, while filters help us select the results we need. They are useful in sales reports and other database queries.

## References

- [PostgreSQL - Aggregate Functions](https://www.postgresql.org/docs/current/functions-aggregate.html)
- [PostgreSQL - Aggregate Function Tutorial](https://www.postgresql.org/docs/current/tutorial-agg.html)
- [PostgreSQL - Table Expressions](https://www.postgresql.org/docs/current/queries-table-expressions.html)
