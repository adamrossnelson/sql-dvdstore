# 🎓 Tutorial: Using ORDER BY in SQLite

## What Is ORDER BY?

In SQLite, the `ORDER BY` clause is used to sort the result set of a query based on one or more columns. This allows you to organize data in a meaningful way, such as alphabetically by name, chronologically by date, or numerically by price.

You can sort in either ascending (lowest to highest) or descending (highest to lowest) order.

---

## Basic Syntax

```sql
SELECT column1, column2
FROM table_name
ORDER BY column1 [ASC|DESC];
```

Use `ASC` for ascending order and `DESC` for descending order. If no order is specified, SQLite uses ascending order by default.

---

## Default Order: ASC vs DESC

Here’s a quick overview of what each keyword does:

* `ASC` (ascending): A to Z, 0 to 9, earliest to latest
* `DESC` (descending): Z to A, 9 to 0, latest to earliest

You can specify the order like this:

```sql
ORDER BY price ASC;
```

or

```sql
ORDER BY release_year DESC;
```

---

## Practical Example: Sorting Results

Let’s work with our `beverage_preferences` table again:

| customer\_name | favorite\_beverage |
| -------------- | ------------------ |
| Alex           | Tea                |
| Jordan         | Coffee             |
| Morgan         | Tea                |
| Casey          | Water              |
| Alex           | Juice              |

### Sort beverages alphabetically

```sql
SELECT customer_name, favorite_beverage
FROM beverage_preferences
ORDER BY favorite_beverage;
```

This returns beverages in alphabetical order.

### Sort beverages in reverse alphabetical order

```sql
SELECT customer_name, favorite_beverage
FROM beverage_preferences
ORDER BY favorite_beverage DESC;
```

---

## Sorting By Multiple Columns

You can also sort by more than one column. This is helpful when there are duplicate values in the first column and you want a secondary sort order.

```sql
SELECT customer_name, favorite_beverage
FROM beverage_preferences
ORDER BY favorite_beverage ASC, customer_name DESC;
```

This first sorts by `favorite_beverage` A to Z, and if multiple people have the same favorite, it sorts their names Z to A.

---

## ORDER BY with WHERE

You can combine `ORDER BY` with `WHERE` to filter and sort in the same query.

```sql
SELECT customer_name, favorite_beverage
FROM beverage_preferences
WHERE favorite_beverage != 'Water'
ORDER BY customer_name ASC;
```

This filters out anyone who chose water and then sorts the rest by name.

---

Yes—great observation! Since all movies in the Sakila dataset have a `release_year` of 2006, sorting by that column doesn’t produce any meaningful variation.

Here's a better challenge that makes use of the `ORDER BY` clause with more useful variation in the Sakila data:

---

##  Challenge

You’re working as a database specialist for a DVD rental store. Your manager wants to better understand the inventory by identifying the longest movies in the collection.

In the Sakila database, the `film` table includes a column called `length`, which represents the duration of each movie in minutes.

Your task is to:

1. Write a query to return the `title` and `length` (and any other columns you think are relevant) of all films - During testing you might consider use of the `limit` clause to limit the number of results returned.
2. Sort the results so the longest movies appear first.
3. Test your query using SQLite and the Sakila database.

When you’re ready, scroll down to see the solution at the bottom of this tutorial.

---

## Summary

* Use `ORDER BY` to sort query results by one or more columns.
* Default sort order is ascending (`ASC`).
* Use `DESC` to reverse the order.
* Combine `ORDER BY` with `WHERE` to filter and sort results.
* Use multiple columns for layered sorting.

---

## Challenge Solution

```sql
SELECT title, length
FROM film
ORDER BY length DESC;
```

This query returns all films sorted by duration from longest to shortest.
