# 🎓 General Intermediate SQL Challenges

Welcome to this intermediate challenge set. These exercises are designed to help you apply what you've learned about GROUP BY, aggregate functions, and HAVING clauses. Each challenge includes:

- A realistic task or business question
- A short hint section to guide you (optional—skip it if you want to try on your own)
- A full solution at the end of each challenge

For best results, break each problem into small parts. If you get stuck, look back at earlier lessons before turning to other tools (before turning to other tools including GenAI).

---

## Challenge 1: Customer Spending Analysis

Your first business task is this:

**Which customers have spent more than $175.00 in total, and how much has each of them spent?**

A plausible business related use case for this query would be identifying high-value customers for a loyalty program or targeted marketing campaign. These are customers who contribute significantly to your revenue stream and might deserve special attention or personalized offers.

Take a moment to try writing this query yourself.

---

### Hint

To solve this, you'll need to:

- Query the `payment` table
- Use `GROUP BY` to group payments by customer
- Use the `SUM()` function to total payment amounts
- Filter groups using `HAVING` with a comparison operator (`>`)
- Order results to show highest spenders first

Find the solution at the bottom of this tutorial.

---

## Challenge 2: Film Length Distribution

The next challenge is this:

**For each film rating (G, PG, etc.), what is the average length of films, and which ratings have an average length greater than 115 minutes?**

A plausible business related use case for this query would be understanding content patterns to optimize scheduling and viewer expectations. Film length affects how many showings can be scheduled per day and how viewers plan their time. Knowing which ratings tend to have longer films helps with both operational planning and customer communications.

---

### Hint

You'll need to:

* Use the `film` table
* Use `GROUP BY` to group films by rating
* Use the `AVG()` function to calculate average length
* Use `HAVING` to filter ratings with average length > 115 minutes
* Order the results to show longest average lengths first

Find the solution at the bottom of this tutorial.

---

## Challenge 3: Active Rental Dates

Your next task:

**On which dates did the store process more than 10 rental transactions, and how many transactions occurred on each of those busy days?**

A plausible business related use case for this query would be identifying peak rental days for staffing purposes. If certain days consistently show higher transaction volumes, management can ensure adequate staff coverage during those times to maintain customer service quality and reduce wait times.

---

### Hint

To solve this, you'll need:

* The `rental` table
* Extract just the date portion using `DATE(rental_date)`
* Use `GROUP BY` with this date expression
* Use `COUNT()` to count transactions per day
* Use `HAVING` to filter for days with more than 10 rentals
* Order results by count in descending order

Find the solution at the bottom of this tutorial.

---

## Challenge 4: Rental Revenue by Movie Rating

Your final challenge for this intermediate tutorial sequence:

**What is the total rental revenue by moving rating category**

A plausible business related use case for this query would be understanding the financial impact of different movie ratings on revenue. This analysis helps identify which rating categories generate the most revenue, which can inform marketing strategies, pricing models, or inventory management decisions. Understanding which ratings are most profitable can guide decisions on which types of content to prioritize or promote more aggressively.

---

### Hint

You'll need:

* The `film` table
* `GROUP BY` to group films by rating
* Aggregate functions to analyze films in each rating category

Find the solution at the bottom of this tutorial.

---

# Solutions Below

### Challenge 1: Solution

**Which customers have spent more than $175.00 in total, and how much has each of them spent?**

```sql
SELECT customer_id, SUM(amount) AS total_spent
FROM payment
GROUP BY customer_id
HAVING total_spent > 175.00
ORDER BY total_spent DESC;
```

This query groups all payments by customer, calculates each customer's total spending, and returns only those who have spent more than $175.00, ordered from highest to lowest spend.

A specific walk through of this query is as follows:

1. `SELECT customer_id, SUM(amount) AS total_spent`: Selects the customer ID and the sum of their total spending. The `SUM()` function is used to calculate the total spending for each customer.
2. `FROM payment`: Selects the payment table.
3. `GROUP BY customer_id`: Groups the payments by customer ID.
4. `HAVING total_spent > 175.00`: Filters the results to only include customers who have spent more than $175.00.
5. `ORDER BY total_spent DESC`: Orders the results by total spending in descending order.

---

### Challenge 2: Solution

**For each film rating (G, PG, etc.), what is the average length of films, and which ratings have an average length greater than 115 minutes?**

```sql
SELECT rating, AVG(length) AS average_length
FROM film
GROUP BY rating
HAVING average_length > 115
ORDER BY average_length DESC;
```

This query groups films by their rating, calculates the average length for each rating, and returns only those ratings where the average film length exceeds 115 minutes.

A specific walk through of this query is as follows:

1. `SELECT rating, AVG(length) AS average_length`: Selects the film rating and the average length of films for each rating. The `AVG()` function is used to calculate the average length for each rating.
2. `FROM film`: Selects the film table.
3. `GROUP BY rating`: Groups the films by their rating.
4. `HAVING average_length > 115`: Filters the results to only include ratings where the average film length exceeds 115 minutes.
5. `ORDER BY average_length DESC`: Orders the results by average film length in descending order.

---

### Challenge 3: Solution

**On which dates did the store process more than 10 rental transactions, and how many transactions occurred on each of those busy days?**

```sql
SELECT DATE(rental_date) AS rental_day, 
       COUNT(*) AS transactions
FROM rental
GROUP BY rental_day
HAVING transactions > 10
ORDER BY transactions DESC;
```

This query extracts just the date portion of the rental_date, groups all rentals by that date, counts how many rentals occurred on each date, and filters to show only dates with more than 10 rental transactions.

A specific walk through of this query is as follows:

1. `SELECT DATE(rental_date) AS rental_day, COUNT(*) AS transactions`: Selects the rental date and the count of rentals for each day. The `DATE()` function is used to extract just the date portion of the rental_date.
2. `FROM rental`: Selects the rental table.
3. `GROUP BY rental_day`: Groups the rentals by the rental day.
4. `HAVING transactions > 10`: Filters the results to only include days with more than 10 rental transactions.
5. `ORDER BY transactions DESC`: Orders the results by the count of rentals in descending order.

---

### Challenge 4: Solution

**What is the total rental revenue by moving rating category**

```sql
SELECT rating,
       COUNT(*) AS film_count,
       SUM(rental_rate) AS total_rental_revenue
FROM film
GROUP BY rating;
```

This query analyzes the film ratings by examining several important metrics without requiring joins. For each rating category, it calculates:

- The number of films in that category
- The total rental revenue generated by films in that category

A specific walk through of this query is as follows:

1. `SELECT rating, COUNT(*) AS film_count, SUM(rental_rate) AS total_rental_revenue`: Selects the film rating and the count of films in each rating category, as well as the total rental revenue generated by films in each rating category.
2. `FROM film`: Selects the film table.
3. `GROUP BY rating`: Groups the films by their rating.
4. `ORDER BY film_count DESC`: Orders the results by the count of films in each rating category in descending order.

This type of multi-dimensional analysis helps understand which rating categories contain more films, command higher rental rates, and represent greater inventory investments.
