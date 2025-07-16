# 🎓 General Capstone Advanced SQL Challenges

Welcome to the general challenge designed to test your knowledge of beginner, intermediate, and advanced SQL. Each challenge includes:

- A realistic task or business question
- A short hint section to guide you
- A full solution at the end of each challenge

For best results, break each problem into small parts. If you get stuck, look back at earlier lessons (before turning to other tools including GenAI).

---

## Challenge 1: High-Value Customers

Your first business task is this:

**Which customers have spent more than $150.00 in total, and how much has each of them spent?**

A plausible business related use case for this query would be identifying high-value customers for a loyalty program or targeted marketing campaign. These are customers who contribute significantly to your revenue stream and might deserve special attention or personalized offers. By understanding your top spenders, you can develop strategies to retain them and encourage similar spending patterns from other customers.

Take a moment to try writing this query yourself.

---

### Hint

To solve this first challenge, you'll most likely need to:

- Query the `payment` table
- Use `GROUP BY` to group payments by customer
- Use the `SUM()` function to total payment amounts
- Filter groups using `HAVING` with a comparison operator (`>`)
- Order results to show highest spenders first

Find the solution at the bottom of this tutorial.

---

## Challenge 2: Popular Rental Categories by Month

The next challenge is:

**For each month of 2005, which film categories had more than 100 rentals, and how many rentals did they have?**

A plausible business related use case for this query would be to analyze seasonal trends in customer preferences. Understanding which categories perform well during different months could inform inventory management, marketing campaigns, and promotional offers. For example, if 'Action' films are especially popular in summer months while 'Family' films see higher rentals during holiday seasons, you could optimize store purchasing and display strategies accordingly.

---

### Hint

You'll need to:

* Use the `rental`, `inventory`, `film_category`, and `category` tables
* Extract the month from rental dates using the `strftime('%m', rental_date)` function
* Use `JOIN` operations to connect these tables
* Use `GROUP BY` with multiple columns (month and category)
* Filter with `HAVING` to show only categories with >100 rentals
* Order the results by month and then by rental count

If you are not already familiar with the `strftime` function its purpose here is to extract a specific part of a date or time value. In this case, we are extracting the month from the rental date. A specific explanation of the `strftime('%m', rental_date)` syntax is that `%m` is a format code that represents the month as a zero-padded decimal number (e.g., '01' for January, '02' for February, etc.).

Find the solution at the bottom of this tutorial.

---

## Challenge 3: Staff Performance Analysis

Your next task:

**Which staff members processed more than $1000 in payments for each month of 2005, and what was their total for each month?**

A plausible business related use case for this query would be performance evaluation and incentive planning. By tracking which staff members consistently exceed revenue thresholds each month, managers can identify top performers for recognition, bonuses, or advancement opportunities. This data could also highlight successful sales techniques that could be shared across the team or reveal patterns in customer service approaches that drive higher sales.

---

### Hint

To solve this, you'll need:

* The `payment` and `staff` tables
* Extract month from payment dates using `strftime('%m', payment_date)`
* `JOIN` to get staff names
* `GROUP BY` both month and staff member
* Use `SUM()` to calculate total payment amounts
* Use `HAVING` to filter for totals > $1000
* Order by month and then by total amount in descending order

Find the solution at the bottom of this tutorial.

---

# Solutions Below

### Challenge 1: Solution

**Which customers have spent more than $150.00 in total, and how much has each of them spent?**

```sql
SELECT c.first_name || ' ' || c.last_name AS customer_name, SUM(p.amount) AS total_spent
FROM payment p
JOIN customer c ON p.customer_id = c.customer_id
GROUP BY p.customer_id, customer_name
HAVING total_spent > 150.00
ORDER BY total_spent DESC;
```

This query groups all payments by customer, calculates each customer's total spending, and returns only those who have spent more than $150.00, ordered from highest to lowest spend.

A specific walk through of this query is as follows:

1. `SELECT c.first_name || ' ' || c.last_name AS customer_name, SUM(p.amount) AS total_spent`: Selects the customer's first and last name, and the sum of their total spending. The `||` operator is used to concatenate the first and last name.
2. `FROM payment p`: Selects the payment table and aliases it as `p`.
3. `JOIN customer c ON p.customer_id = c.customer_id`: Joins the customer table with the payment table on the customer ID.
4. `GROUP BY p.customer_id, customer_name`: Groups the payments by customer ID and customer name.
5. `HAVING total_spent > 150.00`: Filters the results to only include customers who have spent more than $150.00.
6. `ORDER BY total_spent DESC`: Orders the results by total spending in descending order.

---

### Challenge 2: Solution

**For each month of 2005, which film categories had more than 100 rentals, and how many rentals did they have?**

```sql
SELECT strftime('%m', r.rental_date) AS month,
       c.name AS category_name,
       COUNT(*) AS rental_count
FROM rental r
JOIN inventory i ON r.inventory_id = i.inventory_id
JOIN film_category fc ON i.film_id = fc.film_id
JOIN category c ON fc.category_id = c.category_id
WHERE strftime('%Y', r.rental_date) = '2005'
GROUP BY month, category_name
HAVING rental_count > 100
ORDER BY month, rental_count DESC;
```

This query joins several tables to connect rental transactions to film categories. It extracts the month from rental dates, groups by both month and category, and filters to show only categories with more than 100 rentals in each month of 2005.

A specific walk through of this query is as follows:

1. `SELECT strftime('%m', r.rental_date) AS month, c.name AS category_name, COUNT(*) AS rental_count`: Selects the month from rental dates, the category name, and the count of rentals.
2. `FROM rental r`: Selects the rental table and aliases it as `r`.
3. `JOIN inventory i ON r.inventory_id = i.inventory_id`: Joins the inventory table with the rental table on the inventory ID.
4. `JOIN film_category fc ON i.film_id = fc.film_id`: Joins the film_category table with the inventory table on the film ID.
5. `JOIN category c ON fc.category_id = c.category_id`: Joins the category table with the film_category table on the category ID.
6. `WHERE strftime('%Y', r.rental_date) = '2005'`: Filters the results to only include rentals from the year 2005.
7. `GROUP BY month, category_name`: Groups the results by month and category name.
8. `HAVING rental_count > 100`: Filters the results to only include categories with more than 100 rentals.
9. `ORDER BY month, rental_count DESC`: Orders the results by month and rental count in descending order.

---

### Challenge 3: 

**Which staff members processed more than $1000 in payments for each month of 2005, and what was their total for each month?**

```sql
SELECT strftime('%m', p.payment_date) AS month,
       s.first_name || ' ' || s.last_name AS staff_name,
       SUM(p.amount) AS total_amount
FROM payment p
JOIN staff s ON p.staff_id = s.staff_id
WHERE strftime('%Y', p.payment_date) = '2005'
GROUP BY month, p.staff_id
HAVING total_amount > 1000
ORDER BY month, total_amount DESC;
```

This query joins the payment and staff tables, extracts the month from payment dates, and calculates the total payment amount processed by each staff member each month. It then filters to show only staff members who processed more than $1000 in payments in a given month.

A specific walk through of this query is as follows:

1. `SELECT strftime('%m', p.payment_date) AS month, s.first_name || ' ' || s.last_name AS staff_name, SUM(p.amount) AS total_amount`: Selects the month from payment dates, the staff name, and the sum of the total amount.
2. `FROM payment p`: Selects the payment table and aliases it as `p`.
3. `JOIN staff s ON p.staff_id = s.staff_id`: Joins the staff table with the payment table on the staff ID.
4. `WHERE strftime('%Y', p.payment_date) = '2005'`: Filters the results to only include payments from the year 2005.
5. `GROUP BY month, p.staff_id`: Groups the results by month and staff ID.
6. `HAVING total_amount > 1000`: Filters the results to only include staff members who processed more than $1000 in payments in a given month.
7. `ORDER BY month, total_amount DESC`: Orders the results by month and total amount in descending order.

