# Databases PSQL

## ACID

### Atomicity

### Consistency

### Isolation

### Durability

#### Isolation levels

Isolation levels protect the database from anomalous **phenomena**.

>Higher **Isolation Levels** may have slower performance in database transactions due to the need for more locks and more complex concurrency control mechanisms to ensure that transactions are executed in the correct order and that the isolation guarantees are maintained.

>**READ UNCOMMITTED**: This is the lowest isolation level. Transactions at this level can read data that has not yet been committed by other transactions, and they can also read data that is currently being modified by other transactions. This can lead to dirty reads, non-repeatable reads, and phantom reads.

>**READ COMMITTED**: This isolation level ensures that transactions only read data that has been committed by other transactions. It does not prevent other transactions from modifying the data that is being read, which can still lead to non-repeatable reads and phantom reads.

>**REPEATABLE READ**: This isolation level ensures that transactions cannot read data that has been modified or inserted by other transactions, but it does not prevent other transactions from reading the data that is being modified or inserted by the current transaction. This can lead to phantom reads.

>**SERIALIZABLE**: This is the highest isolation level. It ensures that transactions are completely isolated from each other, and that they are executed in a serial order as if they were a single transaction. This can prevent dirty reads, non-repeatable reads, and phantom reads, but it can also lead to higher contention and lower concurrency.

>
#### Phenomena

>**Dirty read**: A dirty read occurs when a transaction reads data that has been modified by another transaction that has not yet been committed. This can lead to inconsistent or invalid data being read by the first transaction, because the changes made by the second transaction may be rolled back or discarded.

>**Non-repeatable** read: A non-repeatable read occurs when a transaction reads the same data multiple times, but the data has been modified by another transaction in between the reads. This can lead to different results being returned each time the data is read, which can be confusing or misleading.

>**Phantom read**: A phantom read occurs when a transaction reads a set of rows that meet a certain criterion, and then another transaction modifies or inserts rows that also meet that criterion, resulting in the first transaction "seeing" additional rows that it did not see before. This can lead to unexpected or undesired results, as the first transaction may not be aware of the additional rows that have been added.


```sql
-- Transaction 1:

SELECT * FROM users WHERE age > 18;
-- Returns: [{id: 1, name: 'Alice', age: 19}, {id: 2, name: 'Bob', age: 21}]

-- Transaction 2:

INSERT INTO users (name, age) VALUES ('Charlie', 19);

-- Transaction 1:

SELECT * FROM users WHERE age > 18;
-- Returns: [{id: 1, name: 'Alice', age: 19}, {id: 2, name: 'Bob', age: 21}, {id: 3, name: 'Charlie', age: 19}]
```

## Indexes

>Indexes are a common way to enhance database performance. An index allows the database server to find and retrieve specific rows much faster than it could do without an index. But indexes also add overhead to the database system as a whole, so they should be used sensibly.

[Indexes - PostgreSQL Documentation](https://www.postgresql.org/docs/current/indexes.html])

### Types

>PostgreSQL provides several index types: B-tree, Hash, GiST, SP-GiST, GIN, BRIN, and the extension bloom.

```sql
CREATE INDEX name ON table USING HASH (column);
```

>By default, the CREATE INDEX command creates B-tree indexes. The other index types are selected by writing the keyword USING followed by the index type name

[Indexes Types - PostgreSQL Documentation]https://www.postgresql.org/docs/current/indexes-types.html]

### ORDER BY

>Only B-tree can produce sorted output. You can adjust the ordering of a B-tree index by including the options ASC, DESC, NULLS FIRST, and/or NULLS LAST when creating the index.

```psql
CREATE INDEX test2_info_nulls_low ON test2 (info NULLS FIRST);
CREATE INDEX test3_desc_index ON test3 (id DESC NULLS LAST);
```

## Database implementation

### Pages

[Storage Page Layout - PostgreSQL Documentation](https://www.postgresql.org/docs/current/storage-page-layout.html)

### Indexes

>An **Index** is another data structure separate from the rows.
>It has part of the data and used to execute queries quicker.
>Indexes are also stored as pages and cost IO operations resources


#### Primary Index AKA clustered Index

>A clustered index is a type of index in a relational database that determines the physical order of the data in a table. Unlike non-clustered indexes, which store only a reference to the data, a clustered index physically reorders the data in a table based on the values in the index columns.

>The clustered index acts as a pointer to the data, and the database can use pointer arithmetic to quickly access the right page in the table, just as you would with an array.

#### Secondary Index

>A secondary index can be created on one or more columns in a table, and it stores the values of the indexed columns along with a reference to the corresponding data in the table. When a query is executed that involves columns that are not part of the primary index, the database can use the secondary index to find the relevant data, rather than having to scan the entire table.

#### Concurrently building Indexes

>PostgreSQL supports building indexes without locking out writes. This method is invoked by specifying the CONCURRENTLY option of CREATE INDEX. When this option is used, PostgreSQL must perform two scans of the table, and in addition it must wait for all existing transactions that could potentially modify or use the index to terminate.

### ROW vs COLUMN Databases

>**Row-based databases** are well-suited to handling transactions and processing large amounts of data in a relational context, while **column-based databases** are better suited to handling large amounts of analytical data and performing complex calculations.

### Primary vs Secondary Keys

#### Primary keys

>The behavior of a RDBMS when inserting new rows into a table depends on several factors, including the type of key used as the primary key and the configuration of the database.

>If for example an auto-incrementing integer or a universally unique identifier (UUID), then the RDBMS can simply append the new row to the end of the table without the need to reorder the existing data.

>If the primary key is a string or a date, the RDBMS might have to reorder the existing data. For example, if the primary key is a string, the RDBMS might have to sort the data alphabetically based on the primary key value. This can slow down the process of inserting new rows.

```sql
/* Define Primary Key to be in descending orders */
CREATE TABLE mytable (
  id TEXT PRIMARY KEY DESC,
  name TEXT,
  ...
);
```

## B-Trees vs B+ Trees

[B tree and B+ tree - Geeks For Geeks](https://www.geeksforgeeks.org/difference-between-b-tree-and-b-tree/)

[Modern B-Tree techniques - Youtube](https://www.youtube.com/watch?v=4ELJDEjDpqk)




