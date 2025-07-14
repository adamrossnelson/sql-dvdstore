# 📀 Getting Started with the Sakila Database using SQLite3

Welcome! This tutorial will guide you through accessing and exploring the "Sakila" database using the `sqlite3` command-line interface (CLI). Read more about this data here in this repository's [Data Acknodlwedgement](https://github.com/adamrossnelson/sql-dvdstore/blob/main/DataAcknowledgement.md).

## 🍎 How To Use This Resource

This repository contains a series of tutorial files organized in a progressive learning path for SQL beginners. Here's how to make the most of these resources:

1. **Start with the basics**: If you're completely new to SQL or need a refresher on setting up SQLite, visit the [SQL Sandbox repository](https://github.com/adamrossnelson/sql-sandbox) first for a lower-level introduction.

2. **Follow the numbered tutorials**: The files are numbered (1010, 1020, etc.) to guide you through SQL concepts in a logical order, from basic queries to more complex filtering and sorting.

3. **Hands-on practice**: For each concept, try the example queries using the included `sakila.db` database file. The best way to learn SQL is by writing and running your own queries.

4. **Complete the challenges**: Each tutorial includes challenges to test your understanding. Try solving these before looking at the provided solutions.

5. **Reference as needed**: Once you're comfortable with the basics, you can use these files as a quick reference for specific SQL techniques.

## 💡 What Is the Sakila Database?

These data are fictional examples of a DVD rental store records. If you're not sure what DVDs are, you're not alone! Before streaming platforms like Netflix and Disney+, people used to rent movies on physical discs (called DVDs) from video rental stores.

Sakila simulates how one of those stores operated — tracking customers, movie inventory, rentals, payments, and more.

Even though DVDs aren’t as common as they once were the data model is realistic and useful for learning SQL.

---

## 🔧 Step 1: Opening the Sakila Database in SQLite

You’ll need:
- A terminal or command prompt
- SQLite installed on your machine
- The `sakila.db` file (make sure it’s in your current directory)

> [!NOTE]
> If you need an introduction to installing and getting oriented with SQLite check out the [SQL Sandbox repository](https://github.com/adamrossnelson/sql-sandbox).

To open the database, run:

```bash
sqlite3 sakila.db
```

You’ll now be inside the `sqlite3` prompt. It looks like this:

```
sqlite>
```

---

## 📋 Step 2: Turn Headers On

By default, SQLite doesn’t show column names when displaying results. Turn them on for easier reading:

```sql
.headers on
```

Also, for better formatting:

```sql
.mode column
```

Now your query results will look more like a table with column headers.

---

## 🔍 Step 3: Explore the Database Schema

To view all tables in the Sakila database:

```sql
.tables
```

You’ll see table names like (among others):

```
actor           customer        film            inventory
category        payment         rental          staff
```

To see the structure (columns and types) of a specific table, use:

```sql
.schema film
```

The `.scheme film` command shows the structure of the `film` table, including column names and types. Notice that the CLI interface shows the structure by displaying SQL code that would recreate the table.

---

## 🧠 What Does the Sakila Data Represent?

A quick rundown of selected tables in these data:

| Table        | What It Represents                                  |
| ------------ | --------------------------------------------------- |
| `film`       | The movies available in the store                   |
| `inventory`  | Each physical DVD copy of each film                 |
| `rental`     | Every time a customer rents a DVD                   |
| `customer`   | People who signed up for a rental account           |
| `staff`      | Employees working at the store                      |
| `store`      | Physical store locations (yes, there were chains!)  |
| `payment`    | How customers paid for their rentals                |
| `actor`      | Actors starring in the films                        |
| `film_actor` | Which actors appeared in which films (many-to-many) |
| `category`   | Movie genres like Action, Comedy, Documentary, etc. |

---

## ✅ Try It Out

Try this simple SQL query to see the first few movies:

```sql
SELECT film_id, title, release_year, rental_rate
FROM film
LIMIT 5;
```

Or list all customers:

```sql
SELECT customer_id, first_name, last_name, email
FROM customer
LIMIT 5;
```

---

## ✅ Overview of Each Tutorial

* [1010 SELECT DISTINCT](1010-SELECT-DISTINCT.md) - Learn how to retrieve unique values from columns, eliminating duplicate results to find distinct categories and options.

* [1020 COUNT](1020-COUNT.md) - Master the COUNT function to quickly summarize data, count records, and analyze quantities in your database tables.

* [1030 SELECT WHERE](1030-SELECT-WHERE.md) - Discover how to filter query results using comparison and logical operators to find specific data matching your criteria.

* [1040 ORDER BY](1040-ORDER-By.md) - Learn to sort your query results in ascending or descending order based on one or more columns for better organization.

* [1050 BETWEEN and IN](1050-BETWEEN-IN.md) - Simplify range-based and multi-value filtering with these operators that make your queries more concise and readable.

* [1060 LIKE](1060-LIKE.md) - Master pattern matching in text data using wildcards to search for partial matches and text patterns.

* [1090 General Beginner Challenges](1090-GENERAL-BEGINNER.md) - Practice your SQL skills with a series of beginner-friendly challenges covering all the concepts you've learned.

---

## 🎉 You’re On Your Way!

You’ve now opened a database, explored its structure, and inspected the data! The Sakila dataset may represent a business model that’s admmittedly no longer common remains apopular resource for learning how relational databases work.

Next step? Try writing some joins to combine tables and answer questions like:

* Which customers rented which movies?
* What are the most popular genres?
* How much revenue did each store make?

Happy querying!
