# SQL Constraints
SQL Constraints are rules applied to columns or tables in a database to ensure the accuracy, integrity, and reliability of the data stored. These constraints enforce specific conditions on the data and control the types of data that can be inserted, updated, or deleted, thereby maintaining the quality and consistency of the database.


## 1. PRIMARY KEY Constraint

- **Definition:** Ensures that each row in a table has a unique identifier. A primary key column cannot contain NULL values.
- **Usage:**
  - Use a primary key to uniquely identify each record in a table.
  - Ensure that primary keys are meaningful and immutable.
- **Limitations:**
  - Only one primary key is allowed per table.
  - The primary key columns must have unique values.
### Syntax:
```sql
CREATE TABLE table_name (
    column1 datatype PRIMARY KEY,
    column2 datatype,
    ...
);
```
### Example:
```sql
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    FirstName VARCHAR(50),
    LastName VARCHAR(50)
);
```
## 2. FOREIGN KEY Constraint

- **Definition:** Ensures that a value in one table must exist in another table. It maintains referential integrity between tables.
- **Usage:**
  - Use foreign keys to maintain relationships between tables and ensure consistency.
  - Enforce cascading updates or deletes if needed.
- **Limitations:**
  - Performance may be affected if foreign key constraints are heavily used, especially in large datasets.
  - Deletes or updates in the parent table may be restricted by foreign key constraints unless cascading options are set.
### Syntax:
```sql
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    ...
    FOREIGN KEY (column1) REFERENCES other_table(column2)
);
```
### Example:
```sql
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    EmployeeID INT,
    FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID)
);
```
## 3. UNIQUE Constraint

- **Definition:** Ensures that all values in a column are unique across the table. It allows NULL values unless explicitly restricted.
- **Usage:**
  - Use unique constraints to enforce the uniqueness of values in one or more columns.
  - Useful for columns that should not have duplicate values (e.g., email addresses).
- **Limitations:**
  - Unique constraints allow NULL values unless specified otherwise, and multiple NULL values are treated as distinct.
  - May impact performance due to additional indexing requirements.
### Syntax:
```sql
CREATE TABLE table_name (
    column1 datatype UNIQUE,
    column2 datatype,
    ...
);
```
### Example:
```sql
CREATE TABLE Products (
    ProductID INT PRIMARY KEY,
    ProductCode VARCHAR(10) UNIQUE
);
```
## 4. NOT NULL Constraint

- **Definition:** Ensures that a column cannot have NULL values. It enforces that a value must be entered for that column.
- **Usage:**
  - Use NOT NULL constraints to ensure that essential columns always have a value.
  - Essential for columns that are critical for the business logic.
- **Limitations:**
  - Cannot be used with columns where NULL values are meaningful.
  - Might require additional handling of NULL values in application logic.
### Syntax:
```sql
CREATE TABLE table_name (
    column1 datatype NOT NULL,
    column2 datatype,
    ...
);
```
### Example:
```sql
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    CustomerName VARCHAR(100) NOT NULL
);
```
## 5. CHECK Constraint

- **Definition:** Ensures that all values in a column satisfy a specific condition or expression.
- **Usage:**
  - Use check constraints to enforce domain integrity by ensuring that column values adhere to specific rules.
  - Suitable for conditions that are simple and can be evaluated by the database.
- **Limitations:**
  - Complex conditions or calculations may not be efficiently handled.
  - Performance can be impacted if used extensively on large datasets.
### Syntax:
```sql
CREATE TABLE table_name (
    column1 datatype NOT NULL,
    column2 datatype,
    ...
);
```
### Example:
```sql
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    CustomerName VARCHAR(100) NOT NULL
);
```
## 6. DEFAULT Constraint

- **Definition:** Provides a default value for a column when no value is specified during insert operations.
- **Usage:**
  - Use default constraints to provide automatic values for columns when no explicit value is given.
  - Ideal for columns where a sensible default value can be defined.
- **Limitations:**
  - Default values should be sensible and align with business logic.
  - May not be suitable for columns that require unique or calculated values.
### Syntax:
```sql
CREATE TABLE table_name (
    column1 datatype DEFAULT default_value,
    column2 datatype,
    ...
);
```
### Example:
```sql
CREATE TABLE Products (
    ProductID INT PRIMARY KEY,
    ProductName VARCHAR(100),
    QuantityInStock INT DEFAULT 0
);
```
## 7. AUTO_INCREMENT Constraint

- **Definition:** Automatically generates a unique value for a column, often used for primary keys. Note: `AUTO_INCREMENT` is specific to MySQL. SQL Server uses `IDENTITY`, and PostgreSQL uses `SERIAL`.
- **Usage:**
  - Use auto-increment constraints to automatically generate unique values for primary key columns.
  - Useful for primary key columns that are sequentially generated.
- **Limitations:**
  - Auto-increment values are generally integers and may need adjustment for non-integer types.
  - Re-seeding or manual changes can be complex and should be done carefully.
### Syntax:
```sql
CREATE TABLE table_name (
    column1 INT AUTO_INCREMENT,
    column2 datatype,
    ...
);
```
### Example:
```sql
CREATE TABLE Orders (
    OrderID INT AUTO_INCREMENT PRIMARY KEY,
    OrderDate DATE
);
```
## 8. Composite Key

- **Definition:** A primary key that consists of more than one column to uniquely identify a row.
- **Usage:**
  - Use composite keys when a single column cannot uniquely identify a row.
  - Ideal for many-to-many relationships where multiple columns are needed for uniqueness.
- **Limitations:**
  - Composite keys can be complex and may impact performance.
  - Should be used when necessary, as simpler primary keys are often preferable.
### Syntax:
```sql
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    ...
    PRIMARY KEY (column1, column2)
);
```
### Example:
```sql
CREATE TABLE OrderDetails (
    OrderID INT,
    ProductID INT,
    Quantity INT,
    PRIMARY KEY (OrderID, ProductID)
);
```
## 9. Index Constraint

- **Definition:** While not technically a constraint, indexing can enforce uniqueness and speed up query performance.
- **Usage:**
  - Use indexes to improve query performance and enforce uniqueness on columns.
  - Essential for frequently queried columns or those used in JOIN operations.
- **Limitations:**
  - Indexes can impact write performance and increase storage requirements.
  - Too many indexes can slow down insert, update, and delete operations.
### Syntax:
```sql
CREATE UNIQUE INDEX index_name
ON table_name (column1, column2);
```
### Example:
```sql
CREATE UNIQUE INDEX idx_product_code
ON Products (ProductCode);
```
## Note

SQL constraints are crucial for maintaining data accuracy, consistency, and integrity. Properly using and understanding the limitations of each constraint ensures that your database remains reliable and efficient.


# SQL Constraints Interview Questions

## Beginner

### 1. What is a SQL constraint, and why is it used?
- **Answer:** A SQL constraint is a rule applied to columns or tables to ensure the accuracy, integrity, and reliability of the data stored in the database. Constraints are used to enforce specific conditions on the data, preventing incorrect data entry and maintaining data quality.

### 2. Can you explain the `NOT NULL` constraint and provide an example?
- **Answer:** The `NOT NULL` constraint ensures that a column cannot have NULL values, meaning that every row must have a value for that column.
- **Example**:
```sql
CREATE TABLE Employees (
    EmployeeID INT NOT NULL,
    Name VARCHAR(100) NOT NULL,
    Position VARCHAR(50)
);
```
In this example, EmployeeID and Name columns cannot have NULL values.

### 3. How does a `PRIMARY KEY` constraint differ from a `UNIQUE` constraint?
- **Answer:** A `PRIMARY KEY` constraint ensures that each row in a table is uniquely identifiable and does not allow NULL values. A `UNIQUE` constraint also ensures uniqueness but allows for NULL values, with multiple NULLs treated as distinct values.

### 4. What is the purpose of the `DEFAULT` constraint, and how is it used?
- **Answer:** The `DEFAULT` constraint provides a default value for a column when no value is specified during an insert operation.
- **Example**:
```sql
CREATE TABLE Products (
    ProductID INT PRIMARY KEY,
    ProductName VARCHAR(100) NOT NULL,
    Price DECIMAL(10, 2) DEFAULT 0.00
);
```
In this example, if no value is provided for the Price column, it will default to 0.00.
## Intermediate

### 1. How do `FOREIGN KEY` constraints help maintain data integrity?
- **Answer:** `FOREIGN KEY` constraints ensure that a value in one table matches a value in another table, thus maintaining referential integrity between related tables. This prevents orphaned records and ensures that relationships between tables are consistent.

### 2. Explain the `CHECK` constraint and give an example of its use.
- **Answer:** The `CHECK` constraint enforces a condition on the values in a column or a set of columns.
- **Example:**
```sql
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    Name VARCHAR(100),
    Age INT CHECK (Age >= 18)
);
```
In this example, the CHECK constraint ensures that the Age column must have a value greater than or equal to 18.

### 3. What is a composite key, and when would you use it?
- **Answer:** A composite key is a primary key that consists of two or more columns to uniquely identify a row in a table. It is used when a single column is not sufficient to uniquely identify records.
- **Example:**
```sql
CREATE TABLE OrderDetails (
    OrderID INT,
    ProductID INT,
    Quantity INT,
    PRIMARY KEY (OrderID, ProductID)
```
Here, OrderID and ProductID together form a composite key to uniquely identify each order detail.

### 4. Describe the impact of constraints on database performance.
- **Answer:** Constraints can impact performance by adding overhead to data manipulation operations. For example, `FOREIGN KEY` constraints might slow down `DELETE` or `UPDATE` operations due to the need to maintain referential integrity. `UNIQUE` and `PRIMARY KEY` constraints can impact performance due to additional indexing. However, constraints are crucial for maintaining data integrity and should be used judiciously.

## Advanced

### 1. How do you handle a situation where you need to drop a constraint, and what are the implications?
- **Answer:** To drop a constraint, you use the `ALTER TABLE` statement with the `DROP CONSTRAINT` clause.
- **Example:**
```sql
ALTER TABLE Employees
DROP CONSTRAINT UC_EmployeeEmail;
```
Dropping a constraint removes the enforced rule, which can lead to data integrity issues if the constraint was ensuring important data quality rules.

### 2. Explain the use of `DEFERRABLE` constraints and provide an example.
- **Answer:** `DEFERRABLE` constraints allow the enforcement of constraints to be postponed until the end of a transaction.This can be useful in complex transactions involving multiple changes.
- **Example:**
```sql
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID) DEFERRABLE INITIALLY DEFERRED
);
```
In this example, the foreign key constraint can be deferred until the transaction is committed.

### 3. What are the differences between `ON DELETE CASCADE`, `ON DELETE SET NULL`, and `ON DELETE RESTRICT` options in foreign key constraints?
- **Answer:** 
  - **ON DELETE CASCADE:** Automatically deletes rows in the child table when the corresponding row in the parent table is deleted.
  - **ON DELETE SET NULL:** Sets the foreign key column in the child table to NULL when the corresponding row in the parent table is deleted.
  - **ON DELETE RESTRICT:** Prevents the deletion of a row in the parent table if there are related rows in the child table, enforcing referential integrity.

### 4. How can you optimize the performance of constraints in a large database?
- **Answer:** To optimize constraint performance:
  - Use appropriate indexes to support constraints, especially for `PRIMARY KEY` and `UNIQUE` constraints.
  - Minimize the use of complex `CHECK` constraints to avoid performance degradation.
  - Regularly monitor and analyze query performance to ensure that constraints are not negatively impacting overall database performance.
  - Consider deferring constraints when working with complex transactions to reduce overhead during individual operations.

