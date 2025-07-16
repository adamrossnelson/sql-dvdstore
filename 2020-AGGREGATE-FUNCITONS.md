# 🎓 Tutorial: Aggregate Functions in SQLite

## What Are Aggregate Functions?

Aggregate functions in SQLite are used to perform calculations on a set of values and return a single summary result. These are especially useful when you want to answer questions like:

- How many items are in a group?
- What’s the average price?
- What’s the total amount spent?
- What’s the highest or lowest value in a column?

Here are the most commonly used aggregate functions:

| Function   | Description                                      |
|------------|--------------------------------------------------|
| `COUNT()`  | Counts the number of rows or non-null values     |
| `SUM()`    | Adds up all the values in a numeric column       |
| `AVG()`    | Returns the average (mean) of numeric values     |
| `MAX()`    | Returns the largest value in a column            |
| `MIN()`    | Returns the smallest value in a column           |

These functions return one value per group when used with `GROUP BY`, or just one value overall if `GROUP BY` is not used.

---

## Additional Considerations

This tutorial is written as an overview, rather than a hands-on walkthrough with detailed examples and also a challenge and solution. Instead this mini-tutorial means to help you pause and think about the concepts behind aggregate functions before continuing with more applied examples.

Here are a few things to keep in mind:

- Aggregate functions ignore nulls by default. For example, `AVG(column_name)` skips rows where the column value is `NULL`.
- `COUNT(*)` counts all rows, including those with `NULL` values.
- You can use aggregate functions without `GROUP BY` if you just want a single summary statistic for the entire table.
- You can also use them with `WHERE` to filter rows before the aggregation happens.

---

### Example 1: Count All Rentals

```sql
SELECT COUNT(*)
FROM rental;
```

This returns the total number of rental transactions.

---

### Example 2: Total Payments by Staff Member

```sql
SELECT staff_id, SUM(amount) AS total_collected
FROM payment
GROUP BY staff_id;
```

This query shows how much each staff member has collected in payments.

---

### Example 3: Average Film Length by Rating

```sql
SELECT rating, AVG(length) AS avg_length
FROM film
GROUP BY rating;
```

This groups all films by rating and computes the average length for each group.

---

## Summary

* Aggregate functions allow you to summarize data across rows.
* They are most powerful when used with `GROUP BY`, but can also be used on their own.
* Common examples include `COUNT()`, `SUM()`, `AVG()`, `MIN()`, and `MAX()`.
* You can use them with or without `WHERE` to control which data gets aggregated.
