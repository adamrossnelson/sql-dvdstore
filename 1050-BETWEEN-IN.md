# 🎓 Tutorial: Using BETWEEN and IN Operators in SQLite

## What Are BETWEEN and IN Operators?

In SQLite, `BETWEEN` and `IN` operators are filtering tools that simplify common `WHERE` clause conditions and make your queries more readable.

- The `BETWEEN` operator selects values within a range (inclusive of the range values).
- The `IN` operator allows you to specify multiple values in a WHERE clause.

These operators save you from writing longer, more complex conditions with multiple `AND` or `OR` clauses.

---

## BETWEEN Syntax

```sql
SELECT column1, column2
FROM table_name
WHERE column_name BETWEEN value1 AND value2;
```

This is equivalent to:

```sql
SELECT column1, column2
FROM table_name
WHERE column_name >= value1 AND column_name <= value2;
```

Notice that the `BETWEEN` operator is inclusive - it includes the boundary values in the results.

---

## Practical Example: BETWEEN with Numbers

Let's use the Sakila database to find films with rental rates in a specific price range.

Imagine you're a customer looking for moderately priced films - not the cheapest, but not premium-priced either. You want films with rental rates between $2.99 and $4.99.

```sql
SELECT title, rental_rate
FROM film
WHERE rental_rate BETWEEN 2.99 AND 4.99
ORDER BY rental_rate;
```

This query returns all films where the rental rate is $2.99, $4.99, or any price in between, ordered by price.

Without `BETWEEN`, you'd need to write:

```sql
SELECT title, rental_rate
FROM film
WHERE rental_rate >= 2.99 AND rental_rate <= 4.99
ORDER BY rental_rate;
```

---

## Using BETWEEN with Dates

The `BETWEEN` operator is especially useful for date ranges. Let's find all rentals that occurred in May 2005:

```sql
SELECT rental_id, rental_date, return_date, inventory_id, customer_id
FROM rental
WHERE rental_date BETWEEN '2005-05-01' AND '2005-05-31'
ORDER BY rental_date;
```

This query returns all rentals where the rental date falls within May 2005.

Note how this query also returns the `inventory_id` and `customer_id` columns. Also note that these columns display numbers instead of movie names or customer names. This is because the `rental` table only contains the IDs of the movies and customers, not their names. To get the names of the movies and customers, we would need to join the `rental` table with the `inventory` and `customer` tables. Which is a topic for a future tutorials.

> [!NOTE]
> When working with dates in SQLite, use the ISO format 'YYYY-MM-DD' for best results. SQLite does not have a separate DATE data type, but stores dates as TEXT, REAL, or INTEGER values.

---

## IN Syntax

```sql
SELECT column1, column2
FROM table_name
WHERE column_name IN (value1, value2, ...);
```

This is equivalent to:

```sql
SELECT column1, column2
FROM table_name
WHERE column_name = value1 OR column_name = value2 OR ...;
```

The `IN` operator checks if a value matches any value in a list of specified values.

---

## Practical Example: IN with Text Values

Suppose you want to find films with specific ratings, like 'PG', 'G', and 'PG-13':

```sql
SELECT title, rating
FROM film
WHERE rating IN ('PG', 'G', 'PG-13')
ORDER BY rating, title;
```

This query finds all films that have any of these three ratings.

> [!NOTE]
> When working in Python there is also an `in` operator that can be used to check if a value is in a list or other iterable. These operations are substantially similar in both Python and SQL.

Without the `IN` operator, you'd have to write:

```sql
SELECT title, rating
FROM film
WHERE rating = 'PG' OR rating = 'G' OR rating = 'PG-13'
ORDER BY rating, title;
```

---

## Using NOT IN

You can also use `NOT IN` to exclude values from your results:

```sql
SELECT title, rating
FROM film
WHERE rating NOT IN ('PG', 'G')
ORDER BY rating;
```

This query returns all films except those rated 'PG' or 'G', which would show films with ratings like 'PG-13', 'R', and 'NC-17'.

---

## Using IN with Numbers

The `IN` operator works with numbers too. Let's find films with specific rental durations:

```sql
SELECT title, rental_duration
FROM film
WHERE rental_duration IN (3, 5, 7)
ORDER BY rental_duration;
```

This finds all films available for rent for exactly 3, 5, or 7 days.

---

## BETWEEN vs Multiple Conditions

Let's compare using `BETWEEN` versus using multiple conditions to find films with lengths between 60 and 90 minutes:

### Using BETWEEN:

```sql
SELECT title, length
FROM film
WHERE length BETWEEN 60 AND 90
ORDER BY length;
```

### Using AND with comparison operators:

```sql
SELECT title, length
FROM film
WHERE length >= 60 AND length <= 90
ORDER BY length;
```

Both queries produce identical results, but the `BETWEEN` version is more concise and readable.

---

## Challenge

You work at a DVD rental store and need to help a customer find films that:

1. Have a rental duration of either 3 or 5 days (not 4 days)
2. Cost between $0.99 and $2.99 to rent

Write a query using both the `IN` and `BETWEEN` operators to find these films. Your results should include the film title, rental duration, and rental rate.

---

## Summary

- The `BETWEEN` operator selects values within a range (inclusive).
- The `IN` operator allows you to specify multiple possible values for a column.
- Both operators make your queries more concise and readable.
- `NOT BETWEEN` and `NOT IN` can be used to exclude ranges or sets of values.
- These operators work with numbers, text, and dates.

---

## Challenge Solution

Here's a solution to the challenge:

```sql
SELECT title, rental_duration, rental_rate
FROM film
WHERE rental_duration IN (3, 5)
AND rental_rate BETWEEN 0.99 AND 2.99
ORDER BY rental_rate, rental_duration;
```

This query combines both operators:
- `IN` to match films with rental durations of exactly 3 or 5 days
- `BETWEEN` to find films with rental rates from $0.99 to $2.99 (inclusive)

The results are ordered first by rental rate (cheapest first), then by rental duration.
