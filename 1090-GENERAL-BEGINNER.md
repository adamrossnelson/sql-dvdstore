# 🎓 General Beginner SQL Challenges

Welcome to this larger general challenge. This is designed to help you apply what you've learned so far. Each challenge includes:

- A realistic task or business question
- A short hint section to guide you (optional—skip it if you want to try on your own)
- A full solution at the end of each challenge

For best results, break each problem into small parts. If you get stuck, look back at earlier lessons (before turning to other tools including GenAI).

---

## Challenge 1: Total High-Value Rentals

Your first business task is this:

**How many rental transactions involved a payment of more than $8.00?**

A plausible business related use case for this query would be identifying high-value rentals that might require special handling or customer service attention. Are you tracking these transactions to ensure they are processed correctly? Do you have a process in place for handling rentals that exceed a certain value? This query could support a review process or alert system.

Take a moment to try writing this query yourself.

---

### Hint

To solve this, you’ll need to:

- Query the `payment` table
- Use the `COUNT()` function to count rows
- Filter rows using `WHERE` with a comparison operator (`>`)

Find the solution at the bottom of this tutorial.

---

## Challenge 2: Last Names Ending in 'son'

The next challenge is this:

**How many customers have a last name that ends in "son"?**

A plausible business related use case for this query would be to explore regional or cultural naming patterns within the customer base—particularly if the store is expanding into new neighborhoods or tailoring marketing campaigns. Ever wonder if certain family name endings suggest a demographic trend? Your manager does, and insights like this could help shape personalized outreach, neighborhood-specific promotions, or even community-focused loyalty programs.

This name ending is common in many regions (like names ending in "Johnson", "Anderson", "Nelson", etc.), and your manager is curious if there’s a pattern.

---

### Hint

You’ll need to:

* Use the `customer` table
* Use `COUNT(*)`
* Use the `LIKE` operator with a wildcard to match names that end in "son"

Find the solution at the bottom of this tutorial.

---

## Challenge 3: Film Titles with Exactly 12 Characters

Your next task:

**How many films have a title that is exactly 12 characters long?**

A plausible business related use case for this query would be to prepare design-friendly displays or digital layouts where film titles of a certain length fit neatly into signage, thumbnails, or column-based grids. Ever built a UI where long or short titles throw off the alignment? Identifying titles with exactly 12 characters can help maintain consistent formatting across promotional materials.

---

### Hint

To solve this, you’ll need:

* The `film` table
* The `LENGTH()` function
* A `WHERE` clause with a comparison operator (`=`)

Find the solution at the bottom of this tutorial.

---

## Challenge 4: Customers with First Names Starting with 'K' or 'L'

Your final challenge for this beginner tutorial sequence:

**How many customers have a first name that starts with either the letter 'K' or the letter 'L'?**

A plausible business related use case for this query would be running a targeted customer appreciation campaign or seasonal promotion—perhaps something playful like “K & L Customer Appreciation Week.” Ever notice how some names pop up more often than others in your customer list? Grouping by name initials can help personalize outreach, create themed marketing efforts, or even test whether certain promotions resonate differently across customer segments.

---

### Hint

You’ll need:

* The `customer` table
* The `LIKE` operator used twice
* The `OR` logical operator

Find the solution at the bottom of this tutorial.

---

# Solutions Below

### Challenge 1: Solution

**How many payment transactions involved a payment of more than $8.00?**

```sql
SELECT COUNT(amount)
FROM payment
WHERE amount > 8.00;
```

This query returns the number of payment transactions where the amount was greater than \$8.00.

A specific walk through of this query is as follows:

1. `SELECT COUNT(amount)`: Selects the count of rows that match the conditions.
2. `FROM payment`: Selects the payment table.
3. `WHERE amount > 8.00`: Filters the results to only include rows where the amount is greater than \$8.00.

---

### Challenge 2: Solution

**How many customers have a last name that ends in "son"?**

```sql
SELECT COUNT(*)
FROM customer
WHERE last_name LIKE '%son';
```

The `%` wildcard matches any number of characters before the `"son"` ending.

A specific walk through of this query is as follows:

1. `SELECT COUNT(*)`: Selects the count of rows that match the conditions.
2. `FROM customer`: Selects the customer table.
3. `WHERE last_name LIKE '%son'`: Filters the results to only include rows where the last name ends with "son".
4. `LIKE '%son'`: Matches last names that end with "son". The `%` wildcard matches any number of characters before the "son" ending.

---

### Challenge 3: Solution

**How many films have a title that is exactly 12 characters long?**

```sql
SELECT COUNT(*)
FROM film
WHERE LENGTH(title) = 12;
```

This query filters films where the title is exactly 12 characters long.

A specific walk through of this query is as follows:

1. `SELECT COUNT(*)`: Selects the count of rows that match the conditions.
2. `FROM film`: Selects the film table.
3. `WHERE LENGTH(title) = 12`: Filters the results to only include rows where the title is exactly 12 characters long.

---

### Challenge 4: Solution

**How many customers have a first name that starts with either the letter 'K' or the letter 'L'?**

```sql
SELECT COUNT(*)
FROM customer
WHERE first_name LIKE 'K%'
   OR first_name LIKE 'L%';
```

This query matches first names that start with either 'K' or 'L' by combining two `LIKE` patterns.

A specific walk through of this query is as follows:

1. `SELECT COUNT(*)`: Selects the count of rows that match the conditions.
2. `FROM customer`: Selects the customer table.
3. `WHERE first_name LIKE 'K%' OR first_name LIKE 'L%'`: Filters the results to only include rows where the first name starts with 'K' or 'L'.
4. `OR`: Combines the two `LIKE` patterns using the `OR` logical operator.
5. `LIKE 'K%'`: Matches first names that start with 'K'. The `%` wildcard matches any number of characters after 'K'.
6. `LIKE 'L%'`: Matches first names that start with 'L'. The `%` wildcard matches any number of characters after 'L'.
