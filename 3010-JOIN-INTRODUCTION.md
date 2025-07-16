# 👶 Beginner SQL Join Tutorial: List Most Recent 10 Rentals with Customer Names and Price

## What Is a JOIN?

In SQLite, a `JOIN` lets you combine rows from two or more tables based on a related column between them. This is useful when different pieces of information are stored across multiple tables, but you want to bring them together in one query result.

A `JOIN` typically connects tables using a foreign key, which is a column that links one table to another.

The most common type is the `INNER JOIN`, which only includes rows where there is a matching value in both tables.

---

## The General Syntax

Think of database tables as separate spreadsheets. A JOIN is like using glue to stick these spreadsheets together side by side, matching up rows that have the same value in a specific column.

For those familiar with other programming language a join is often otherwise called a merge or concatentation operation. The principles from other languages generally apply to SQL JOINs also.

The basic JOIN syntax looks like this:

```sql
SELECT columns_you_want
FROM first_table
JOIN second_table ON first_table.matching_column = second_table.matching_column;
```

Let's break this down step by step:

1. **SELECT columns_you_want**: List the columns you want to see in your results. You can pick columns from either table.

2. **FROM first_table**: Start with your main table (the one you care about most).

3. **JOIN second_table**: Add the second table you want to bring in.

4. **ON first_table.matching_column = second_table.matching_column**: This is the most important part - it tells SQL how to match up the rows between tables. It's like saying "connect these tables wherever this value in the first table equals this value in the second table."

For clarity, we often use the table name with a dot before each column name (like `customer.customer_id`) to show which table the column comes from. This is especially important when both tables have columns with the same name.

There are several types of JOINs, but the most common is the INNER JOIN (often just written as JOIN), which only keeps rows that have matches in both tables. If a row in the first table doesn't have a matching row in the second table, that row won't appear in your results.

---

## Four Kinds of Joins (INNER, LEFT, RIGHT, and OUTER)

### INNER JOIN

The INNER JOIN returns only the rows that have matching values in both tables. If a row in the first table doesn't have a matching row in the second table, that row won't appear in your results.

Here is how an INNER JOIN would look given the following tables:

**TABLE 1**

| id | name | age | grade | hobby |
|----|------|-----|-------|-------|
| 1 | John | 25 | A | Basketball |
| 2 | Jane | 30 | B | Tennis |
| 3 | Bob | 35 | C | Football |

**TABLE 2**

| id | name | job | state | school |
|----|------|-----|-------|-------|
| 1 | John | Teacher | New York | Harvard |
| 2 | Jane | Nurse | California | Stanford |
| 4 | Alice | Doctor | Texas | Yale |

**INNER JOIN**

| id | name | age | grade | hobby | job | state | school |
|----|------|-----|-------|-------|-----|-------|--------|
| 1 | John | 25 | A | Basketball | Teacher | New York | Harvard |
| 2 | Jane | 30 | B | Tennis | Nurse | California | Stanford |

### LEFT JOIN

The LEFT JOIN returns all the rows from the left table (the table specified first in the JOIN clause), and the matching rows from the right table. If there is no match, the result is NULL on the side of the right table.

Here is how a LEFT JOIN would look given the following tables:

**TABLE 1**

| id | name | age | grade | hobby |
|----|------|-----|-------|-------|
| 1 | John | 25 | A | Basketball |
| 2 | Jane | 30 | B | Tennis |
| 3 | Bob | 35 | C | Football |

**TABLE 2**

| id | name | job | state | school |
|----|------|-----|-------|-------|
| 1 | John | Teacher | New York | Harvard |
| 2 | Jane | Nurse | California | Stanford |
| 4 | Alice | Doctor | Texas | Yale |

**LEFT JOIN**

| id | name | age | grade | hobby | job | state | school |
|----|------|-----|-------|-------|-----|-------|--------|
| 1 | John | 25 | A | Basketball | Teacher | New York | Harvard |
| 2 | Jane | 30 | B | Tennis | Nurse | California | Stanford |
| 3 | Bob | 35 | C | Football | NULL | NULL | NULL |

### RIGHT JOIN

The RIGHT JOIN returns all the rows from the right table (the table specified second in the JOIN clause), and the matching rows from the left table. If there is no match, the result is NULL on the side of the left table.

Here is how a RIGHT JOIN would look given the following tables:

**TABLE 1**

| id | name | age | grade | hobby |
|----|------|-----|-------|-------|
| 1 | John | 25 | A | Basketball |
| 2 | Jane | 30 | B | Tennis |
| 3 | Bob | 35 | C | Football |

**TABLE 2**

| id | name | job | state | school |
|----|------|-----|-------|-------|
| 1 | John | Teacher | New York | Harvard |
| 2 | Jane | Nurse | California | Stanford |
| 4 | Alice | Doctor | Texas | Yale |

**RIGHT JOIN**

| id | name | age | grade | hobby | job | state | school |
|----|------|-----|-------|-------|-----|-------|--------|
| 1 | John | 25 | A | Basketball | Teacher | New York | Harvard |
| 2 | Jane | 30 | B | Tennis | Nurse | California | Stanford |
| 4 | Alice | NULL | NULL | NULL | Doctor | Texas | Yale |

### OUTER JOIN

The OUTER JOIN returns all the rows from both tables, even if there is no match. If there is no match, the result is NULL on the side of the table that doesn't have a match.

Here is how an OUTER JOIN would look given the following tables:

**TABLE 1**

| id | name | age | grade | hobby |
|----|------|-----|-------|-------|
| 1 | John | 25 | A | Basketball |
| 2 | Jane | 30 | B | Tennis |
| 3 | Bob | 35 | C | Football |

**TABLE 2**

| id | name | job | state | school |
|----|------|-----|-------|-------|
| 1 | John | Teacher | New York | Harvard |
| 2 | Jane | Nurse | California | Stanford |
| 4 | Alice | Doctor | Texas | Yale |

**OUTER JOIN**

| id | name | age | grade | hobby | job | state | school |
|----|------|-----|-------|-------|-----|-------|--------|
| 1 | John | 25 | A | Basketball | Teacher | New York | Harvard |
| 2 | Jane | 30 | B | Tennis | Nurse | California | Stanford |
| 3 | Bob | 35 | C | Football | NULL | NULL | NULL |
| 4 | Alice | NULL | NULL | NULL | Doctor | Texas | Yale |

---

## Practical Example: Most Recent 10 Rentals With Customer Names and Price

Let’s say your manager wants to see the most recent 10 rental transactions—including who rented the movie and how much they paid. This is a use case for a `JOIN`.

Here’s what we need:

- Customer name (from the `customer` table)
- Rental timestamp (from the `rental` table)
- Payment amount (from the `payment` table)

We can assume that each rental has one corresponding payment. So, we can use `rental_id` to connect these tables.

### Step-by-step Query:

To build this query (shown above) the approach first identifies the key tables involved: rental for rental activity, customer for the renter’s name, and payment for the amount paid. Using INNER JOIN, it connects these tables based on shared identifiers (customer_id and rental_id) to bring together the necessary information. It then uses ORDER BY rental_date DESC to sort the rentals from most recent to oldest, and applies LIMIT 10 to return only the ten most recent rentals.

```sql
SELECT
  rental.rental_id,
  customer.first_name,
  customer.last_name,
  rental.rental_date,
  payment.amount
FROM rental
INNER JOIN customer ON rental.customer_id = customer.customer_id
INNER JOIN payment ON rental.rental_id = payment.rental_id
ORDER BY rental.rental_date DESC
LIMIT 10;
```

This query first connects `rental` to `customer` using the `customer_id` column, then connects to `payment` using the `rental_id` column. The result shows the 10 most recent rentals with customer names and payment amounts.

---

## Challenge: Film Rentals with Category and Staff Information

Your manager now wants more detailed information about film rentals. They've asked you to create a report that shows:

1. The film title and category (genre) for each rental
2. Which staff member processed the rental
3. The rental date and return date
4. The payment amount

Your challenge is to write a query that joins multiple tables to retrieve this information for the 15 most recently rented films that have already been returned.

### Hint:

You'll need to join several tables:
- `rental` - for rental and return dates
- `inventory` - to link rentals to films
- `film` - to get film titles
- `film_category` - to link films to categories
- `category` - to get category names
- `staff` - to get staff names
- `payment` - to get payment amounts

Try building the query step by step, testing each join as you go.

Find the solution at the bottom of this tutorial.

---

## Summary

* `JOIN` operations allow you to combine data from multiple related tables
* An `INNER JOIN` returns only rows that have matching values in both tables
* Foreign keys are commonly used to establish relationships between tables
* Multiple joins can be chained together to connect several tables in one query
* Always include clear join conditions using the `ON` keyword

---

## Challenge Solution

```sql
SELECT
  film.title AS film_title,
  category.name AS category,
  staff.first_name || ' ' || staff.last_name AS staff_name,
  rental.rental_date,
  rental.return_date,
  payment.amount
FROM rental
INNER JOIN inventory ON rental.inventory_id = inventory.inventory_id
INNER JOIN film ON inventory.film_id = film.film_id
INNER JOIN film_category ON film.film_id = film_category.film_id
INNER JOIN category ON film_category.category_id = category.category_id
INNER JOIN staff ON rental.staff_id = staff.staff_id
INNER JOIN payment ON rental.rental_id = payment.rental_id
WHERE rental.return_date IS NOT NULL
ORDER BY rental.rental_date DESC
LIMIT 15;
```

This query joins seven tables together to get comprehensive information about film rentals:

1. We start with the `rental` table and join it to `inventory` to connect rentals to specific inventory items
2. We then join to `film` to get the film titles
3. The `film_category` and `category` joins allow us to retrieve the film's genre
4. The `staff` join provides information about which employee processed the rental
5. Finally, the `payment` join gives us the amount paid for each rental

We filter to include only rentals that have been returned using `WHERE rental.return_date IS NOT NULL`, sort by rental date, and limit to the 15 most recent returns.
