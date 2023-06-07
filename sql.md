# SQL

## `SELECT`

In SQL, comparisons involving NULL values typically result in unknown or NULL, which means that the condition 2 != referee_id will not be true for rows where referee_id is NULL.


## Misc

### You can use weird casing
```sql
SELECt name
frOm Customer
WhErE 2 != referee_id;
```