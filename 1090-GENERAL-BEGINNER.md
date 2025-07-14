# 🎓 General Beginner SQL Challenges

Welcome to this larger general challenge. This is designed to help you apply what you've learned so far. Each challenge includes:

- A realistic task or business question
- A short hint section to guide you (optional—skip it if you want to try on your own)
- A full solution at the end of each challenge

Don’t hesitate to break each problem into small parts. If you get stuck, look back at earlier lessons (before turning to other tools including GenAI).

---

## Challenge 1: Total High-Value Rentals

Your first business task is this:

**How many rental transactions involved a payment of more than $8.00?**

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

---

### Hint

You’ll need:

* The `customer` table
* The `LIKE` operator used twice
* The `OR` logical operator

Find the solution at the bottom of this tutorial.

---

### Challenge 1: Solution

```sql
SELECT COUNT(amount)
FROM payment
WHERE amount > 8.00;
```

This query returns the number of payment transactions where the amount was greater than \$8.00.

---

### Challenge 2: Solution

```sql
SELECT COUNT(*)
FROM customer
WHERE last_name LIKE '%son';
```

The `%` wildcard matches any number of characters before the `"son"` ending.

---

### Challenge 3: Solution

```sql
SELECT COUNT(*)
FROM film
WHERE LENGTH(title) = 12;
```

This query filters films where the title is exactly 12 characters long.

---

### Challenge 4: Solution

```sql
SELECT COUNT(*)
FROM customer
WHERE first_name LIKE 'K%'
   OR first_name LIKE 'L%';
```

This query matches first names that start with either 'K' or 'L' by combining two `LIKE` patterns.
