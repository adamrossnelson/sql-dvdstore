# 🎓 Tutorial: Using SELECT DISTINCT in SQLite

## What Is SELECT DISTINCT?

In SQLite, the `SELECT DISTINCT` statement is used when you want to return only unique values from a column. This is helpful when a column contains repeated values, and you're only interested in knowing which distinct entries exist.

The general syntax is:

```sql
SELECT DISTINCT column_name
FROM table_name;
````

You can optionally add parentheses around the column name for clarity:

```sql
SELECT DISTINCT (column_name)
FROM table_name;
```

Both versions work the same in SQLite.

---

## Why Use DISTINCT?

Imagine you have a table of customers who have each selected a favorite beverage. Here's a sample of what the data in a table called `beverage_preferences` might look like:

| customer\_name | favorite\_beverage |
| -------------- | ------------------ |
| Alex           | Tea                |
| Jordan         | Coffee             |
| Morgan         | Tea                |
| Casey          | Water              |
| Alex           | Juice              |

This table shows that "Alex" appears twice (perhaps two people named Alex or one person who changed their answer). But if you're only interested in the unique beverage options, you don’t want to see duplicate "Tea" entries.

### Example: Get All Unique Beverages

To get the distinct beverage choices from the `favorite_beverage` column, you would use:

```sql
SELECT DISTINCT favorite_beverage
FROM beverage_preferences;
```

This might return:

```
Coffee
Juice
Tea
Water
```

This tells you that there were four different beverages chosen.

---

## A Word of Caution

If you query something like:

```sql
SELECT DISTINCT customer_name
FROM beverage_preferences;
```

You will get a list of unique customer names. However, this doesn’t tell you whether these are truly different people or the same person listed multiple times. For example, two different people named "Alex" will still appear only once in the result.

---

## Additional Example: Multiple Columns

You can also use `DISTINCT` with more than one column. In that case, SQLite will return unique combinations of those columns.

```sql
SELECT DISTINCT customer_name, favorite_beverage
FROM beverage_preferences;
```

This returns only the unique pairs of customer name and beverage.

---

## Challenge

Imagine you are a database specialist working for a DVD rental store. Your manager wants to better understand the variety of movie ratings available in the store’s collection.

They’re not interested in the full details of every film just yet—they simply want to know: What are the unique ratings of all the films we carry?

In the Sakila database, the `film` table contains a column called `rating`, which includes values like `'PG'`, `'R'`, `'G'`, and so on. These ratings may appear multiple times since many films share the same rating.

Your task:

1. Use `SELECT DISTINCT` to return a list of all unique film ratings from the `film` table.
2. Test your query in SQLite.
3. Confirm that your query returns each rating only once, without any duplicates.

Once you’ve completed the challenge, scroll to the bottom of this tutorial to check your answer under the heading:

---

## Summary

* Use `SELECT DISTINCT` to eliminate duplicate values from your query results.
* Works with one or more columns.
* Helps you focus on unique entries in a dataset.
* Common use cases: finding unique categories, tags, options, or identifiers.

---

## Challenge Solution

To return all unique film ratings from the `film` table, the query is:

```sql
SELECT DISTINCT rating
FROM film;
```

A plausible business related use case for this query is to understand the variety of movie ratings available in the store’s collection. Are you offering a balanced mix of family-friendly content, teen favorites, and more mature titles? Do your shelves reflect the preferences of your customers? This kind of insight can help the store make informed decisions about what to stock, how to organize genres, and which ratings to emphasize in promotions. On your own, consider what other business questions this query might help answer—perhaps about content gaps or customer demand by rating category.

