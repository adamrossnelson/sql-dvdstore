
# 🎓 Tutorial: Using SELECT ... WHERE in SQLite

## What Is SELECT ... WHERE?

In SQLite, the `SELECT` statement is used to retrieve data from a table, and the `WHERE` clause is used to filter that data based on specific conditions. Together, they let you ask questions like:

- Which customers prefer tea?
- Which movies are rated 'PG-13'?
- Which rentals occurred after a specific date?

These are the most commonly used SQL clauses and appear in nearly every query you'll write.

The basic syntax looks like this:

```sql
SELECT column1, column2
FROM table_name
WHERE condition;
```

The `WHERE` clause appears immediately after the `FROM` clause and filters the rows returned based on the given condition.

---

## Comparison Operators

In most cases, you’ll want to compare values using standard operators. These are the same concepts you may have seen Python or R, Excel, or other programmatic contexts (though the syntax may vary).

| Operator | Meaning                  |
| -------- | ------------------------ |
| `=`      | Equals                   |
| `!=`     | Not equal                |
| `>`      | Greater than             |
| `<`      | Less than                |
| `>=`     | Greater than or equal to |
| `<=`     | Less than or equal to    |

These allow you to create filters like:

* Where the beverage is equal to 'Tea'
* Where the rating is not equal to 'R'
* Where the price is greater than 2.99

---

## Logical Operators

You can combine multiple conditions using logical operators These behave similarly to what you're familiar with in Python or R and again other programmtic contexts.

| Operator | Meaning                             |
| -------- | ----------------------------------- |
| `AND`    | Both conditions must be true        |
| `OR`     | At least one condition must be true |
| `NOT`    | Negates the condition that follows  |

---

## Example: Filtering Beverage Choices

Let’s go back to our hypothetical `beverage_preferences` table:

| customer\_name | favorite\_beverage |
| -------------- | ------------------ |
| Alex           | Tea                |
| Jordan         | Coffee             |
| Morgan         | Tea                |
| Casey          | Water              |
| Alex           | Juice              |

### Query 1: Select all rows where the favorite beverage is Tea

This query would be useful if you had a special promotion for tea drinkers. You could use it to send them a coupon or email blast.

```sql
SELECT customer_name, favorite_beverage
FROM beverage_preferences
WHERE favorite_beverage = 'Tea';
```

### Query 2: Select all rows where the beverage is not Water

```sql
SELECT customer_name, favorite_beverage
FROM beverage_preferences
WHERE favorite_beverage != 'Water';
```

### Query 3: Select rows where the beverage is either Tea or Coffee

```sql
SELECT customer_name, favorite_beverage
FROM beverage_preferences
WHERE favorite_beverage = 'Tea' OR favorite_beverage = 'Coffee';
```

---

## Challenge 1

You are a database specialist at a DVD rental store. Your manager wants to identify all movies that are suitable for general audiences. In the Sakila database, the `film` table includes a column called `rating`.

Your task:

1. Write a query to return the `title` and `rating` of all films where the rating is `'G'`.
2. Test your query using SQLite and the Sakila database.

Once you're ready, scroll down to the heading:

---

## Challenge 2

Now your manager wants to find all longer films that might be better suited for older audiences. The `film` table includes a column called `length` (in minutes) and another column called `rating`.

Your task:

1. Write a query to return the `title`, `length`, and `rating` of all films that are **over 120 minutes long** and rated either `'PG-13'` or `'R'`.
2. Test your query using SQLite.

When you're done, scroll down to:

---

## Summary

* Use `SELECT ... WHERE` to filter rows from a table based on specific conditions.
* Combine conditions with comparison operators like `=`, `!=`, `<`, and `>`.
* Use logical operators `AND`, `OR`, and `NOT` to form more complex queries.
* The `WHERE` clause is one of the most important tools in writing meaningful SQL.

---

## Challenge Solution 1

```sql
SELECT title, rating
FROM film
WHERE rating = 'G';
```

This returns all films rated for general audiences.

---

## Challenge Solution 2

```sql
SELECT title, length, rating
FROM film
WHERE length > 120
  AND (rating = 'PG-13' OR rating = 'R');
```

This returns all films over 120 minutes long that are rated PG-13 or R.

```
