# Self Join

## Employees table

```bash
| id | employee | manager |
|----|----------|---------|
| 1  | a        |         |
| 2  | b        | 1       |
| 3  | c        | 2       |

```

### Expected output:
```bash
| id | employee | manager |
|----|----------|---------|
| 1  | a        |   Null  |
| 2  | b        | a       |
| 3  | c        | b       |
```

```sql
SELECT 
    e.id,
    e.employee
    m.employee as manager
FROM
    employees e
LEFT JOIN
    employees m ON e.manager = m.id

```