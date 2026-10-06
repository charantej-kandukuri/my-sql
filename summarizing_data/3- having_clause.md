# HAVING Clause

## D/W WHERE AND HAVING CLAUSE
We use `WHERE` clause **before** we group our rows. We can reference any columns in WHERE clause even if it is not part of the SELECT clause.

We use `HAVING` clause **after** we group our rows. The columns that we use in HAVING clause have to be part of SELECT clause.

We have invoices table.
 invoice_id | invoice_total | client_id 
------------|---------------|-----------
 1          | 100           | 1         
 2          | 200           | 2         
 3          | 500           | 3         
 4          | 200           | 1         


Write a query to get all clients who spent more than 500 and having invoices more then 5.

```sql
SELECT
    client_id
    SUM(invoice_total) AS total_sales
    COUNT(*) AS number_of_invoices
FROM invoices
GROUP BY client_id
HAVING total_sales > 500 AND no_of_invoices > 5 -- having clause

```

## Excercise
Get the customers \
located in Virginia \
who have spent more then $100

```sql
SELECT
    c.customer_id,
    c.first_name
    c.last_name,
    SUM(oi.quantity * oi.unit_price) AS total_sales
FROM customers c
JOIN orders o USING (customer_id)
JOIN order_items io USING (order_id)
WHERE state = "VA"
GROUP BY 
    c.customer_id,
    c.first_name
    c.last_name;
HAVING total_sales > 100
```
