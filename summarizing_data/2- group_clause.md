# Group Clause

```sql
SELECT
    customer_id, -- step 2 -- expose col for view!
    SUM(invoice_total) AS total_sales
FROM invoices
WHERE invoice_date >= '2019-07-01' -- step 3: filter
GROUP BY client_id -- step 1: group by
ORDER BY total_sales DESC -- step 4: sort
```

## Steps
1. Add `GROUP BY` clause on a column.
2. Add to `SELECT` if need to show on the view. _(Optional)_
3. Add filter - if requirement asks
4. sort - if requirement asks 

## Example
Write a query to summerize the sales by state and city

1. firstly, since we need sales by state and city, we need to group the things by state and city
```sql
SELECT 
    SUM(invoice_total) as total_sales
FROM invoices
JOIN clients USING (customer_id)
GROUP BY state, city -- step 1
```

2. secondly expose the colums so we can view them
```sql
SELECT
    state, city, -- step 2
    SUM(invoice_total) AS  total_sales
FROM invoices
JOIN clinets USING (client_id)
GROUP BY state, city
```

## Excercise
Find out the total payments made by each payment_method each day.
### Expected Solution
| date       | payment_method | total_payments |
|------------|----------------|----------------|
| 2019-01-03 | Credit Card    | 74.55          |
| **2019-01-08** | **Credit Card**    | 32.77          |
| **2019-01-08** | **Cash**           | 10             |
| 2019-01-11 | Credit Card    | 0.03           |
| 2019-01-15 | Credit Card    | 148.41         |
| 2019-01-26 | Credit Card    | 87.44          |
| 2019-02-12 | Credit Card    | 8.18           |

### solution
```sql
SELECT
    date,
    pm.name AS payment_method.
    SUM(payment) as total_payments 
FROM payments p
JOIN payment_methods pm ON p.payment_method = pm.payment_method_id
GROUP BY date, payment_method
ORDER BY date
```