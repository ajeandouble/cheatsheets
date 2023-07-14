# SQL

## `SELECT`

In SQL, comparisons involving NULL values typically result in unknown or NULL, which means that the condition 2 != referee_id will not be true for rows where referee_id is NULL.


## Misc

### SQL clauses from a functional programming PoV

- **FROM:** convert Table to array of objects (`prop_name === column name`)
- **WHERE:** -> `table.filter(row => filter_func)`
- **GROUP BY:** -> `table.reduce(row => reduce_func)`
	(means that the grouped property will have a scalar value while the non-aggregated properties will yield an array. Hence the need for aggregating function)
- SELECT -> map
- ORDER BY/LIMIT (slicer)

### You can use weird casing
```sql
SELECt name
frOm Customer
WhErE 2 != referee_id;
```