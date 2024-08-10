# **Azure SQL Index Documentation**

## **Introduction to Indexes**
Indexes in Azure SQL Database are special database objects that improve the speed of data retrieval operations by organizing data in a way optimized for specific query patterns.

## **Types of Indexes**

### **1. Rowstore Index**
- **What It Is**: A general term for indexes that store data in a row-oriented format, where all columns of a row are stored together in a single data page.
- **Key Points**:
  - Data is stored row by row, which is optimal for transactional workloads.
  - Includes **Clustered** and **Non-Clustered** indexes.
- **Use Case**: Best suited for Online Transaction Processing (OLTP) workloads where queries often access full rows of data.

### **2. Clustered Index (a type of Rowstore Index)**
- **What It Is**: Determines the physical order of data in a table. The table is stored in the order of the clustered index key.
- **Key Points**:
  - Only one clustered index per table.
  - The data rows themselves are stored in the index order.
- **Use Case**: Ideal for range queries (e.g., `ORDER BY`, `GROUP BY`) and when the table is frequently queried in a sorted order.

### **3. Non-Clustered Index (a type of Rowstore Index)**
- **What It Is**: A separate structure from the actual data, containing key values and pointers to the data rows.
- **Key Points**:
  - A table can have multiple non-clustered indexes.
  - Data is not stored in the index order; only the index keys are.
- **Use Case**: Improves performance for queries that search for specific values or ranges but don’t need sorted data.

### **4. Unique Index**
- **What It Is**: Ensures that all values in the indexed column(s) are unique, preventing duplicate entries.
- **Key Points**:
  - Can be applied to both clustered and non-clustered indexes.
- **Use Case**: Enforcing data integrity, such as unique email addresses.

### **5. Filtered Index**
- **What It Is**: A non-clustered rowstore index that includes only a subset of the table’s rows, based on a filter condition.
- **Key Points**:
  - Reduces the size of the index.
  - Optimizes specific queries with common filters.
- **Use Case**: Efficient for columns with sparse data or specific values, like only active records.

### **6. Full-Text Index**
- **What It Is**: Supports full-text queries on character-based columns, allowing searches for specific words and phrases.
- **Key Points**:
  - Used for complex text search capabilities.
- **Use Case**: Searching large text fields, like product descriptions or document content.

### **7. Spatial Index**
- **What It Is**: Indexes spatial data types, such as `geography` and `geometry`.
- **Key Points**:
  - Optimizes queries involving spatial data.
- **Use Case**: Geospatial applications, like finding points within a given area.

### **8. Columnstore Index**
- **What It Is**: Stores data in a column-oriented format, which is highly compressed and optimized for analytic queries.
- **Key Points**:
  - Ideal for read-heavy workloads.
  - Significantly improves performance for large-scale data analytics.
- **Use Case**: Data warehousing and business intelligence applications.

### **9. XML Index**
- **What It Is**: Optimizes queries against XML data types.
- **Key Points**:
  - Includes primary and secondary XML indexes.
- **Use Case**: Efficiently querying XML data within the database.

## **Creating and Managing Indexes**

### **Creating an Index**
To create an index in Azure SQL, use the `CREATE INDEX` statement. For example:

```sql
-- Create a Non-Clustered Index
CREATE INDEX IX_Employee_LastName
ON Employees (LastName);
```
## Dropping an Index

To remove an index, use the `DROP INDEX` statement:

```sql
-- Drop an Index
DROP INDEX IX_Employee_LastName ON Employees;
```
### Rebuilding and Reorganizing Indexes
To maintain index performance, especially for rowstore indexes, you can periodically rebuild or reorganize them:

## Rebuild Index: Completely drops and recreates the index.

```sql
ALTER INDEX IX_Employee_LastName ON Employees REBUILD;
```
## Reorganize Index: Defragments the index by reorganizing the leaf level.

```sql
ALTER INDEX IX_Employee_LastName ON Employees REORGANIZE;
```
### Monitoring Indexes
## Checking Index Usage
Azure SQL provides Dynamic Management Views (DMVs) to monitor index usage and fragmentation. For example:

```sql
-- Check Fragmentation Level
SELECT 
    index_id, 
    index_type_desc, 
    avg_fragmentation_in_percent 
FROM sys.dm_db_index_physical_stats (DB_ID(), OBJECT_ID('Employees'), NULL, NULL, 'DETAILED');
```
## Identifying Unused Indexes
You can identify unused indexes that may be taking up unnecessary space:
```sql
-- Find Unused Indexes
SELECT 
    name AS index_name, 
    s.name AS table_name 
FROM sys.indexes i
JOIN sys.tables s ON i.object_id = s.object_id
LEFT JOIN sys.dm_db_index_usage_stats u 
    ON i.object_id = u.object_id AND i.index_id = u.index_id
WHERE u.index_id IS NULL AND i.type_desc = 'NONCLUSTERED';
```
## Best Practices
- **Avoid Over-Indexing**: Too many indexes can slow down INSERT, UPDATE, and DELETE operations and increase storage requirements.
- **Regular Maintenance**: Regularly rebuild or reorganize indexes to avoid performance degradation due to fragmentation.
- **Monitor and Adjust**: Use DMVs to monitor index performance and adjust as needed.
## Note:
Rowstore indexes are fundamental for optimizing transaction processing and scenarios where full rows are frequently accessed. Understanding and maintaining them properly ensures optimal performance in Azure SQL.

# SQL Indexing Interview Questions

## Beginner

### 1. What is an index in SQL, and why is it used?

**Answer:**
An index in SQL is a database object that speeds up data retrieval operations. It works by creating a data structure that allows for quick access to rows in a table based on the indexed columns. Indexes help improve query performance, especially when dealing with large tables.

### 2. What is a clustered index?

**Answer:**
A clustered index determines the physical order of data in a table. The table's data is sorted and stored based on the clustered index key. Each table can have only one clustered index.

### 3. What is a non-clustered index?

**Answer:**
A non-clustered index creates a separate structure from the data that contains a sorted list of the indexed columns along with pointers to the actual data. A table can have multiple non-clustered indexes.

### 4. How do you create a basic index on a table?

**Answer:**
You can create a basic index using the `CREATE INDEX` statement. For example:

```sql
-- Create a Non-Clustered Index
CREATE INDEX IX_Employee_LastName ON Employees(LastName);
```
## Intermediate

### 5. What is the difference between a clustered index and a non-clustered index?

**Answer:**
- **Clustered Index**: Determines the physical order of data in the table. Each table can have only one clustered index.
- **Non-Clustered Index**: Creates a separate structure from the data. It does not affect the physical order of data and a table can have multiple non-clustered indexes.

### 6. What is index fragmentation and why is it a problem?

**Answer:**
Index fragmentation occurs when the index becomes disordered, leading to inefficient data retrieval. This happens when rows are inserted, updated, or deleted, causing gaps or out-of-order pages in the index. Fragmentation can degrade performance and increase storage requirements.

### 7. How do you check index fragmentation in SQL Server?

**Answer:**
You can check index fragmentation using Dynamic Management Views (DMVs). For example:

```sql
-- Check Fragmentation Level
SELECT 
    index_id, 
    index_type_desc, 
    avg_fragmentation_in_percent 
FROM sys.dm_db_index_physical_stats (DB_ID(), OBJECT_ID('Employees'), NULL, NULL, 'DETAILED');
```
### 8. What is the purpose of a filtered index?
**Answer:**
A filtered index is a non-clustered index that includes a subset of rows based on a filter condition. It improves performance and reduces the size of the index by indexing only those rows that meet specific criteria.

## Advanced

### 9. How do you decide when to rebuild or reorganize an index?

**Answer:**
- **Rebuild**: When the index fragmentation level is high (typically above 30%). Rebuilding is more thorough and helps to reclaim disk space.
- **Reorganize**: When the fragmentation level is moderate (typically between 10% and 30%). Reorganizing is less resource-intensive and can be performed more frequently.

### 10. What are columnstore indexes, and when would you use them?

**Answer:**
Columnstore indexes store data in a column-oriented format rather than row-oriented. They are highly compressed and optimized for read-heavy, analytical queries that scan large volumes of data. They are ideal for data warehousing and business intelligence workloads.

### 11. How can you identify unused indexes in SQL Server, and why is it important?

**Answer:**
You can identify unused indexes using DMVs. For example:

```sql
-- Find Unused Indexes
SELECT 
    name AS index_name, 
    s.name AS table_name 
FROM sys.indexes i
JOIN sys.tables s ON i.object_id = s.object_id
LEFT JOIN sys.dm_db_index_usage_stats u 
    ON i.object_id = u.object_id AND i.index_id = u.index_id
WHERE u.index_id IS NULL AND i.type_desc = 'NONCLUSTERED';
```
Identifying and removing unused indexes is important because it reduces storage overhead and improves performance by reducing the number of indexes that need to be maintained.

### 12. What are some advanced strategies for indexing large tables to improve query performance?
**Answer:**

- **Partitioning**: Split a large table into smaller, more manageable pieces to improve query performance and maintenance.
- **Composite Indexes**: Create indexes on multiple columns to optimize queries that filter on multiple columns.
- **Indexed Views**: Use indexed views (materialized views) to pre-compute and store aggregated or joined data for faster retrieval.
- **Columnstore Indexes**: Utilize columnstore indexes for analytic queries that involve large datasets and complex aggregations.
