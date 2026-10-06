# The ROLLUP Opearator

This is used to **Summerize** data.

The **ROLLUP** Operator only applies to **columns that aggregate values**.

This is **limited** to MySQL, not executable in SQL or Oracle.

## 1. GROUP BY single column
```sql
SELECT
    client_id,
	SUM(invoice_total) as total_sales
FROM invoices
GROUP BY client_id WITH ROLLUP
ORDER BY total_sales
```

### Output
|client_id|total_sales|
|---------|-----------|
|2|101.79|
|3|705.90|
|1|802.89|
|5|980.02|
||2590.60|



## 2. When GROUP BY multiple coloumns

```sql
SELECT
	state,
	city,
	SUM(invoice_total) as total_sales
FROM invoices
JOIN clients c USING (client_id)
GROUP BY state, city WITH ROLLUP
ORDER BY total_sales
```

### Output

|state|city|total_sales|
|-----|----|-----------|
|WV|Huntington|101.79|
|WV||101.79|
|CA|San Francisco|705.90|
|CA||705.90|
|NY|Syracuse|802.89|
|NY||802.89|
|OR|Portland|980.02|
|OR||980.02|
|||2590.60|


## Exercise
### Expected output
| payment_method | total  |
|----------------|--------|
| Cash           | 10     |
| Credit Card    | 351.38 |
|                | 361.38 |

### Solution

Lets start simple

#### Step 1: Always start simple first with No JOINS etc.
```sql
SELECT
    payment_method,
    SUM(amount) AS total
FROM payments
GROUP BY payment_method WITH ROLLUP;

```
Output:

|payment_method|total|
|--------------|-----|
|1|351.38|
|2|10.00|
||361.38|

#### Step 2: Lets JOIN to get payment_method name
```sql
SELECT
	pm.name AS payment_method,
	SUM(p.amount) AS total
FROM
	payments p
JOIN payment_methods pm ON
	p.payment_method = pm.payment_method_id
GROUP BY
	pm.name WITH ROLLUP;
```
Output:
|payment_method|total|
|----|-------------|
|Cash|10.00|
|Credit Card|351.38|
||361.38|

_**Note:** When we user WITH ROLLUP in the query we can use the name alias to GROUP BY, in other words in the above query GROUP BY payment_method will give us error._
