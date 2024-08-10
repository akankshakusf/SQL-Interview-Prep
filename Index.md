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
