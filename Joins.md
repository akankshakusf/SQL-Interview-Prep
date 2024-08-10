
# SQL Joins

## 1. INNER JOIN
**Description**: Returns only the rows that have matching values in both tables.
**Example**:
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

## 2. LEFT JOIN (LEFT OUTER JOIN)
**Description**: Returns all the rows from the left table, and the matched rows from the right table. If no match is found, NULL values are returned for columns from the right table.
**Example**:
```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```

## 3. RIGHT JOIN (RIGHT OUTER JOIN)
**Description**: Returns all the rows from the right table, and the matched rows from the left table. If no match is found, NULL values are returned for columns from the left table.
**Example**:
```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```

## 4. FULL JOIN (FULL OUTER JOIN)
**Description**: Returns all the rows when there is a match in either left or right table. Rows without a match in either table will return NULLs for columns from the table without a match.
**Example**:
```sql
SELECT columns
FROM table1
FULL JOIN table2
ON table1.column = table2.column;
```

## 5. CROSS JOIN
**Description**: Returns the Cartesian product of the two tables, i.e., it returns all possible combinations of rows from both tables.
**Example**:
```sql
SELECT columns
FROM table1
CROSS JOIN table2;
```

## 6. SELF JOIN
**Description**: A self-join is a regular join, but the table is joined with itself. It is useful when you need to compare rows within the same table.
**Example**:
```sql
SELECT A.columns, B.columns
FROM table A, table B
WHERE A.column = B.column;
```

## 7. OUTER APPLY
**Description**: Similar to a LEFT JOIN but specifically used to join with table-valued functions. It returns all the rows from the outer table and the matching rows from the table-valued function.
**Example**:
```sql
SELECT columns
FROM table1
OUTER APPLY table2_function(table1.column);
```

## 8. CROSS APPLY
**Description**: Similar to an INNER JOIN but used with table-valued functions. It returns rows where the table-valued function returns a result.
**Example**:
```sql
SELECT columns
FROM table1
CROSS APPLY table2_function(table1.column);
```

These joins allow you to query data in flexible ways, depending on how you want to combine the data from different tables.

# Additional SQL Joins

In addition to the standard joins discussed earlier, there are some other specialized or less common joins that are present in SQL, though they may not be supported by all SQL databases. These include:

## 1. NATURAL JOIN
**Description**: A NATURAL JOIN automatically joins tables based on columns with the same names and data types in both tables. It eliminates the need to specify the join condition explicitly.
**Note**: Not all SQL databases support NATURAL JOIN.
**Example**:
```sql
SELECT *
FROM table1
NATURAL JOIN table2;
```

## 2. SEMI JOIN
**Description**: Semi Join queries are generally executed in the form of subqueries where rows are picked up only from the first (left) table with respect to a condition (or a set of conditions) that is matched in the second table. Unlike regular joins, which include the matching rows from both tables, a semi-join only includes columns from the left table in the result.

A SEMI JOIN returns rows from the first table where one or more matches are found in the second table, but unlike an INNER JOIN, it does not return any columns from the second table.
**Example**:
```sql
SELECT columns
FROM table1
WHERE EXISTS (SELECT 1 FROM table2 WHERE table1.column = table2.column);
```

## 3. ANTI JOIN
**Description**: Anti-joins, also known as anti-semi-joins, are the exact opposite of semi-joins. In Anti Join, rows are picked up from the first table with respect to a condition (or a set of conditions) that is not matched in the second table.

An ANTI JOIN returns rows from the first table where no match is found in the second table. This can be implemented using NOT EXISTS or LEFT JOIN combined with IS NULL.
**Example (using NOT EXISTS)**:
```sql
SELECT columns
FROM table1
WHERE NOT EXISTS (SELECT 1 FROM table2 WHERE table1.column = table2.column);
```

**Example (using LEFT JOIN and IS NULL)**:
```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column
WHERE table2.column IS NULL;
```

## 4. THETA JOIN
**Description**: A THETA JOIN is a type of join that allows you to join tables based on any condition other than equality. It is a generalized form of a join that can use operators like >, <, !=, etc., in the join condition.
**Example**:
```sql
SELECT columns
FROM table1
JOIN table2
ON table1.column > table2.column;
```

## 5. EQUI JOIN
**Description**: An EQUI JOIN is a specific type of join where the condition is based on equality between the columns of the tables. This is essentially what an INNER JOIN usually does.
**Example**:
```sql
SELECT columns
FROM table1
JOIN table2
ON table1.column = table2.column;
```

## 6. SELF JOIN
**Description**: A SELF JOIN joins a table to itself. It's useful when you need to compare rows within the same table.
**Example**:
```sql
SELECT A.column1, B.column2
FROM table A, table B
WHERE A.id = B.parent_id;
```

## 7. PARTITIONED OUTER JOIN
**Description**: A PARTITIONED OUTER JOIN is used in some advanced SQL databases to partition data and perform a join operation within each partition. It's often used in data warehousing contexts.
**Example**: This is more of a conceptual join and might require specific syntax depending on the SQL implementation.

## 8. MERGE JOIN
**Description**: In some databases, a MERGE JOIN is a specific join algorithm used by the query optimizer for INNER and OUTER joins when the joined columns are already sorted.
**Note**: This is more about the execution plan rather than a distinct SQL command.

## 9. HASH JOIN
**Description**: Similar to MERGE JOIN, a HASH JOIN is an algorithm used to perform joins when dealing with large, unsorted datasets. The SQL engine may automatically choose a hash join strategy, especially for INNER joins.
**Note**: This is related to query optimization and is not directly written in SQL syntax.

These joins and join strategies allow you to write complex queries to extract and manipulate data based on your specific needs in SQL.
