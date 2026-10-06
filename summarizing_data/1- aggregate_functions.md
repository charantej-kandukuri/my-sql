# Aggregate functions

|  Aggreagte Functions
|---------|
| MAX()   |
| MIN()   |
| AVG()   |
| SUM()   |
| COUNT() |


## Example
```sql
SELECT
    MIN(invoice_total)
    MAX(invoice_total)
    AVG(invoice_total)
    SUM(invoice_total * 0.1) -- expression
    COUNT(invoice_total) -- Total non-null rows - total sales
    COUNT(payment_total) -- Total non-null rows - total payments
    COUNT(*) -- Total records in invoices table
FROM invoices

```

By default null rows are ignored (not counted).
By default all aggregate functions takes "duplicate values", to exclude we have to use "DISTINCT" keyword.

```sql
COUNT (DISTINCT clinet_id) AS total_clients
```

## Excercise
#### Expected output:
| date_range              | total_sales | total_payments | what are expected |
|-------------------------|-------------|----------------|-------------------|
| First Half of the Year  | 2000        | 1500           | 500               |
| Second Half of the Year | 3000        | 2000           | 1000              |
| Total                   | 5000        | 3500           | 1500              |

_Hint: use `UNION` operator to JOIN multiple SELECT queries_ 

#### Solution:
```sql
SELECT
    'First Half of the Year' as 'date_range',
    SUM(invoice_total) as total_sales,
    SUM(payment_total) as total_payment,
    SUM(invoice_total - payment_total) as what_are_expected
FROM invoices
WHERE invoice_date is BETWEEN '01-01-2019' AND '30-06-2019'

UNION

SELECT
    'First Half of the Year' as 'date_range',
    SUM(invoice_total) as total_sales,
    SUM(payment_total) as total_payment,
    SUM(invoice_total - payment_total) as what_are_expected
FROM invoices
WHERE invoice_date is BETWEEN '01-06-2019' AND '31-12-2019'

UNION

SELECT
    'First Half of the Year' as 'date_range',
    SUM(invoice_total) as total_sales,
    SUM(payment_total) as total_payment,
    SUM(invoice_total - payment_total) as what_are_expected
FROM invoices
WHERE invoice_date is BETWEEN '01-01-2019' AND '31-12-2019'
```