# 🎓 Tutorial: Using HAVING in SQLite

## What Is HAVING?

In SQLite, the `HAVING` clause is used to filter the results of a `GROUP BY` query after the aggregation step has occurred. This is different from `WHERE`, which filters rows before they are grouped.

Use `HAVING` when you want to apply a condition to a grouped result—such as only showing customers who made more than 30 rentals or categories with more than 50 items.

The basic structure looks like this:

```sql
SELECT column_name, aggregate_function(column_name)
FROM table_name
GROUP BY column_name
HAVING aggregate_function(column_name) condition;
```

---

## Practical Example: Customers With More Than 30 Rentals

Let’s look at a realistic business question. Suppose your manager wants to know which customers are especially active.

The `rental` table logs each rental transaction. We can count how many rentals each customer made using `GROUP BY`, then use `HAVING` to return only those customers who made more than 37 rentals.

```sql
SELECT customer_id, COUNT(*) AS rental_count
FROM rental
GROUP BY customer_id
HAVING rental_count > 37;
```

This query groups all rental records by customer, counts how many rentals each customer made, and filters the list to show only customers who rented more than 30 times.

Another example in this tutorial series solved this business problem using the the a sorting strategy and also the `LIMIT` clause. It is common in SQL, and in many programming languages, to find many solutions for the same goal.

---

## Challenge

Your manager now wants to understand rental behavior over time.

They ask:

Which return dates had a surge in activity—say, initially say something like more than 50 rentals rented on that date?

Your task is to:

1. Write a query that groups all rental records by `rental_date`.
2. Count how many rentals were rented on each date.
3. Use `HAVING` to filter only the dates where the count was high.
4. Experiment with different threshold values (like 40, 50, 60, or even much much higher) to determine the best cutoff for identifying key 12-15 rental dates with high activity.

Your manager will use the report you build to plan staffing schedules and also potentially for marketing purposes to offer discounts or special promotions on those dates.

> [!NOTE]
> Not yet discussed in these tutorials is the `DATE()` function. This function is used to extract the date part of a datetime value. In this case, it is used to group the rental records by the date part of the `rental_date` column. You will need to use this special function in the solution to this challenge. If you have refrained from generative AI tools thus far, good for you. Consider using generative AI to help you understand more about the `DATE()` function and how to use it in this query.

When you’re ready, scroll down to see the suggested solution for this challenge.

---

## Summary

* Use `HAVING` to filter groups **after aggregation**.
* Use `WHERE` to filter rows **before aggregation**.
* `HAVING` is essential when working with `GROUP BY` and aggregate functions.
* Great for filtering by totals, averages, maximums, or dates after `COUNT()`, `SUM()`, or `MAX()` has been applied.

---

## Challenge Solution

```sql
SELECT DATE(rental_date) AS rental_day, COUNT(*) AS num_rentals
FROM rental
GROUP BY rental_day
HAVING num_rentals > 390;
```

This query returns only those `return_date` values where more than 50 rentals were returned. You can experiment with the `HAVING num_returns > 390` line to explore different thresholds and decide what qualifies as a “busy” return day.

Try values like 40, 60, or even 100 to fine-tune your analysis. These types of queries are especially useful for spotting patterns in customer behavior or preparing staffing schedules for busy days.

A plausible business related use case for this query would be identifying peak rental periods to plan staffing schedules or prepare for high-traffic days. Ever notice how some days are busier than others at your store? By spotting these patterns, you can ensure you have enough staff to handle the rush, whether it’s during holiday seasons, movie releases, or special events. This can help prevent checkout lines from getting too long or ensure you have enough cashiers to handle the volume. On your own, consider how adjusting the thresholds might help shape different retention strategies.
