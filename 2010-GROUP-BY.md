# 🎓 Tutorial: Using GROUP BY in SQLite

## What Is GROUP BY?

In SQLite, the `GROUP BY` clause is used to group rows that share a common value in one or more columns. It's often used with aggregate functions like `COUNT()`, `SUM()`, `AVG()`, `MIN()`, or `MAX()` to summarize data for each group.

For example, you might want to:
- Count how many rentals each customer has made
- Find the total revenue collected by each staff member
- Calculate the number of films in each movie rating category

The basic syntax looks like this:

```sql
SELECT column_name, aggregate_function(column_name)
FROM table_name
GROUP BY column_name;
```

---

## Practical Example: Grouping

Let’s look at two practical examples using the Sakila DVD rental database.

---

### Example 1: Number of Films in Each Rating Category

The `film` table contains a `rating` column with values like `'G'`, `'PG'`, `'PG-13'`, and `'R'`. You can use `GROUP BY` to count how many films fall under each rating:

```sql
SELECT rating, COUNT(*) AS film_count
FROM film
GROUP BY rating;
```

This query returns a list of ratings and the number of films in each rating category.

---

### Example 2: Number of Rentals Per Customer

The `rental` table tracks each rental transaction. To count how many rentals each customer has made:

```sql
SELECT customer_id, COUNT(*) AS rental_count
FROM rental
GROUP BY customer_id;
```

This groups all rental records by customer ID and counts how many rentals each customer has made. 

> [!NOTE]
> As was the case in ealier tutorials, the `customer_id` column is not a unique identifier for a customer. It is a foreign key that references the `customer` table. Future tutorials that cover `join` operations will show you how to combine the `rental` and `customer` tables to get the customer names.

---

## Challenge

Your manager wants to better understand customer rental behavior.

They’ve asked you to write two queries based on what you’ve already learned. Starting with the "Number of Rentals Per Customer" query, make two extensions:

1. **Top Renters**
   Write a query that returns the 10 customers who rented the most movies, with ties broken by the most recent rental date. In other words, if two customers rented the same number of films, list the one who rented more recently first.

2. **Low-Activity Customers**
   Write a query that returns the 10 customers who rented the fewest movies, again using the most recent rental date as a tiebreaker.

Both queries should return the following columns:

* `customer_id`
* Total number of rentals
* Most recent rental date

---

## Summary

* Use `GROUP BY` to group rows that share the same value in a column.
* Commonly used with aggregate functions like `COUNT()` or `MAX()`.
* Helps summarize, categorize, and analyze patterns in your data.
* Can be combined with `ORDER BY` and `LIMIT` for sorted summaries.

---

## Challenge Solutions

---

### Solution 1: Top Renters

```sql
SELECT customer_id,
       COUNT(*) AS rental_count,
       MAX(rental_date) AS last_rental
FROM rental
GROUP BY customer_id
ORDER BY rental_count DESC, last_rental DESC
LIMIT 10;
```

This query groups rentals by customer, counts the total rentals, and finds each customer’s most recent rental. The results are sorted to show the top 10 customers with the most rentals, with ties broken by the most recent activity.

---

### Solution 2: Low-Activity Customers

```sql
SELECT customer_id,
       COUNT(*) AS rental_count,
       MAX(rental_date) AS last_rental
FROM rental
GROUP BY customer_id
ORDER BY rental_count ASC, last_rental DESC
LIMIT 10;
```

This query is nearly the same, but it uses `ORDER BY rental_count ASC` to show customers with the fewest rentals first. As before, it uses the most recent rental as a tiebreaker.

A plausible business related use case for this query would be identifying low-activity customers who may benefit from re-engagement efforts, such as targeted discounts or reminder emails. Have these customers forgotten about your service—or are they just one good recommendation away from returning? By focusing on those who have rented the fewest times but were still active recently, your team can prioritize outreach to customers who are more likely to come back. On your own, consider how adjusting the LIMIT or rental thresholds might help shape different retention strategies.
