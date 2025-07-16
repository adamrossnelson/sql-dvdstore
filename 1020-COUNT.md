# 🎓 Tutorial: Using COUNT in SQLite

## What Is COUNT?

In SQLite, the `COUNT` function is used to return the number of rows that match a given condition. It's one of the most useful tools for quickly summarizing data and answering questions like:

- How many records are in this table?
- How many customers made a rental?
- How many unique categories are there?

The basic syntax looks like this:

```sql
SELECT COUNT(*)
FROM table_name;
```

Or, to count values in a specific column:

```sql
SELECT COUNT(column_name)
FROM table_name;
```

> [!NOTE]
> `COUNT` requires parentheses because it is a function. Unlike some keywords that work with or without parentheses (like `DISTINCT`), `COUNT` will not work without them.

---

## Practical Example: Counting Rows

Let’s reuse our earlier example of a table called `beverage_preferences` that tracks customer drink choices.

| customer\_name | favorite\_beverage |
| -------------- | ------------------ |
| Alex           | Tea                |
| Jordan         | Coffee             |
| Morgan         | Tea                |
| Casey          | Water              |
| Alex           | Juice              |

If we want to know how many rows are in this table, we can run:

```sql
SELECT COUNT(*)
FROM beverage_preferences;
```

This will return:

```
5
```

Because there are 5 rows total.

We can also count a specific column, like:

```sql
SELECT COUNT(customer_name)
FROM beverage_preferences;
```

Or:

```sql
SELECT COUNT(favorite_beverage)
FROM beverage_preferences;
```

All of these will return the same result—`5`—since each row has a value in both columns.

---

## When to Use COUNT(column\_name)

Even though `COUNT(*)` is most common, sometimes it's helpful to use a specific column name. This can make your query easier to understand later when reviewing your code.

In some cases, you might want to count only non-null values in a column. Unlike `COUNT(*)`, which includes every row, `COUNT(column_name)` ignores rows where the column is `NULL`.

---

## Challenge

Imagine you work at a DVD rental store and your manager wants to know how many rental transactions have occurred overall. They want a quick summary of the total number of times any customer has rented a film—regardless of what movie or who the customer was.

In the Sakila database, the `rental` table tracks each rental transaction, and each row in that table represents one rental.

Your task:

1. Write a query that uses `COUNT` to return the total number of rental transactions.
2. Use either `COUNT(*)` or `COUNT(rental_id)`—they should return the same value.
3. Test your query in SQLite using the `sakila.db` database.

When you're ready, scroll down to see the answer under the heading:

---

## Summary

* The `COUNT` function returns the number of rows that match a query.
* Use `COUNT(*)` to count all rows, or `COUNT(column_name)` to count non-null values in a specific column.
* Parentheses are required when using `COUNT`.
* Useful for totals, summaries, and understanding the size of a dataset.

---

## Challenge Solution

To count the total number of rental transactions from the `rental` table, use:

```sql
SELECT COUNT(*)
FROM rental;
```

Or:

```sql
SELECT COUNT(rental_id)
FROM rental;
```

Both queries return the same result, since `rental_id` is a required, non-null field for each row in the table.

A plausible business use case for this query is to understand the total number of rental transactions in the store’s collection. On your own, consider what other business questions this query might help answer. What other counts might be useful to know for you or your manager?
