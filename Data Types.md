# DataType:
A data type is an attribute that specifies the type of data that the object can hold.

## Numeric Data Types

- **INT**: 4-byte integer.  
  - Stores integer values. Range: -2,147,483,648 to 2,147,483,647.

- **BIGINT**: 8-byte integer.  
  - Stores large integer values. Range: -2^63 to 2^63-1.

- **SMALLINT**: 2-byte integer.  
  - Stores smaller integer values. Range: -32,768 to 32,767.

- **TINYINT**: 1-byte integer.  
  - Stores very small integer values. Range: 0 to 255.

- **FLOAT**: Floating point number with approximate precision.  
  - Stores approximate numeric values with floating decimal points. Precision can be up to 53 bits.

- **REAL**: Single-precision floating point number.  
  - Stores approximate numeric values with single-precision (32-bit) floating points.

- **DECIMAL(p, s)**: Fixed-point number with precision `p` and scale `s`.  
  - Stores exact numeric values with fixed precision (`p`) and scale (`s`). Precision can be up to 38 digits.

- **NUMERIC(p, s)**: Same as DECIMAL.  
  - Functionally identical to DECIMAL, storing exact numeric values with fixed precision (`p`) and scale (`s`).

## Date and Time Data Types

- **DATE**: Date value (year, month, day).  
  - Stores date values. Range: 0001-01-01 to 9999-12-31.

- **TIME**: Time of day.  
  - Stores time values (hour, minute, second, fractional seconds). Range: 00:00:00.0000000 to 23:59:59.9999999.

- **DATETIME**: Date and time with a precision of 3.33 milliseconds.  
  - Stores date and time values. Range: 1753-01-01 to 9999-12-31.

- **DATETIME2**: Date and time with up to 7 digits of fractional seconds precision.  
  - Stores date and time values with higher precision. Range: 0001-01-01 to 9999-12-31.

- **SMALLDATETIME**: Date and time with a precision of 1 minute.  
  - Stores date and time values. Range: 1900-01-01 to 2079-06-06.

- **DATETIMEOFFSET**: Date and time with time zone offset.  
  - Stores date and time values with time zone offset information. Range: 0001-01-01 to 9999-12-31, with offsets from -14:00 to +14:00 hours.

## Character and String Data Types

- **CHAR(n)**: Fixed-length character string with length `n`.  
  - Stores fixed-length non-Unicode characters. Length specified by `n` (1-8,000).

- **VARCHAR(n)**: Variable-length character string with maximum length `n`.  
  - Stores variable-length non-Unicode characters. Maximum length is `n` (1-8,000) or VARCHAR(MAX) for up to 2 GB.

- **TEXT**: Variable-length character data (deprecated in favor of VARCHAR(MAX)).  
  - Stores large variable-length non-Unicode data.

- **NCHAR(n)**: Fixed-length Unicode character string with length `n`.  
  - Stores fixed-length Unicode characters. Length specified by `n` (1-4,000).

- **NVARCHAR(n)**: Variable-length Unicode character string with maximum length `n`.  
  - Stores variable-length Unicode characters. Maximum length is `n` (1-4,000) or NVARCHAR(MAX) for up to 2 GB.

- **NTEXT**: Variable-length Unicode character data (deprecated in favor of NVARCHAR(MAX)).  
  - Stores large variable-length Unicode data.

## Binary Data Types

- **BINARY(n)**: Fixed-length binary data with length `n`.  
  - Stores fixed-length binary data. Length specified by `n` (1-8,000).

- **VARBINARY(n)**: Variable-length binary data with maximum length `n`.  
  - Stores variable-length binary data. Maximum length is `n` (1-8,000) or VARBINARY(MAX) for up to 2 GB.

- **IMAGE**: Variable-length binary data (deprecated in favor of VARBINARY(MAX)).  
  - Stores large binary data.

## Other Data Types

- **BIT**: Integer data type that can be 0, 1, or NULL.  
  - Stores Boolean values (0 or 1).

- **UNIQUEIDENTIFIER**: Globally unique identifier (GUID).  
  - Stores globally unique identifiers in a 16-byte value.

- **XML**: XML data type for storing XML data.  
  - Stores XML data. Allows for querying and modification using SQL Server’s XML functions.

- **JSON**: JSON data type (handled as NVARCHAR, but Azure SQL has JSON functions for parsing and querying).  
  - Stores JSON-formatted strings using NVARCHAR. Supports querying and manipulating JSON data with SQL Server JSON functions.

# SQL Data Types - Interview Questions

## Basic Questions

1. **What is the difference between `CHAR` and `VARCHAR` data types?**
   - *Follow-up*: When would you use one over the other?

2. **What are the key differences between `INT`, `BIGINT`, `SMALLINT`, and `TINYINT`?**
   - *Follow-up*: In what scenarios would you use `BIGINT` over `INT`?

3. **Explain the difference between `FLOAT` and `DECIMAL`.**
   - *Follow-up*: Why would you choose `DECIMAL` for storing financial data?

4. **What is the difference between `DATETIME` and `DATETIME2`?**
   - *Follow-up*: How does `DATETIMEOFFSET` enhance the functionality of `DATETIME`?

5. **How do `BINARY` and `VARBINARY` differ in terms of storage and use cases?**

## Intermediate Questions

6. **What are the limitations of the `TEXT` and `NTEXT` data types, and why are they deprecated?**
   - *Follow-up*: What alternatives does SQL offer for handling large text data?

7. **How does the `UNIQUEIDENTIFIER` data type work, and what are its typical use cases?**
   - *Follow-up*: What are the performance implications of using `UNIQUEIDENTIFIER` as a primary key?

8. **Explain the use and benefits of the `XML` data type in SQL.**
   - *Follow-up*: How does SQL Server's handling of XML data differ from handling JSON data?

9. **What are the differences between `SMALLDATETIME` and `DATETIME` in terms of precision and storage?**
   - *Follow-up*: In what scenarios would `SMALLDATETIME` be preferable?

10. **How can you store and query JSON data in Azure SQL Database?**
    - *Follow-up*: What are the benefits and limitations of using JSON data types compared to traditional relational data structures?

## Advanced Questions

11. **What is the impact of using different precision and scale values in `DECIMAL(p, s)` on storage and performance?**

12. **Discuss how the `BIT` data type is stored and its practical applications in a database schema.**
    - *Follow-up*: What are the considerations when using `BIT` for large datasets?

13. **How does SQL Server handle the storage of Unicode data in `NCHAR` and `NVARCHAR` compared to `CHAR` and `VARCHAR`?**
    - *Follow-up*: What are the performance implications of using Unicode data types?

14. **Can you explain the concept of sparse columns in SQL Server, and how do they relate to data types?**
    - *Follow-up*: What are the advantages and disadvantages of using sparse columns?

15. **What are the storage requirements for the `DATE`, `TIME`, `DATETIME`, `DATETIME2`, and `DATETIMEOFFSET` data types?**
    - *Follow-up*: How do these differences in storage impact database performance and design?
