# Index types

___

**Q: What types of indexes are there in SQL?**

In order to make lookups faster, SQL databases employ indexes.

Indexes contain keys built from one or more columns. They can either be clustered or non-clustered.

Clustered index alters the table by sorting rows based on their key values. There can only be one clustered index per table because the data can be sorted only in one way at a time.

Non-clustered index resides outside of the table and represents a mapping of an index key to a row. There can be multiple non-clustered indexes per table because they don't affect the table structure.

Both type of indexes can be configured as unique, in which case rows are not allowed to have duplicate key values.

Indexes are automatically maintained when the table is modified.

## Composite Indexes

Composite (or compound) indexes are created on multiple columns of a table. They're particularly useful for queries that filter on multiple columns together.

### Key characteristics:
- Created on two or more columns in a specific order
- Follow the "leftmost principle" - can be used for queries referencing the leading columns
- More selective than single-column indexes for certain query patterns
- Larger in size than single-column indexes

### Example:
```sql
CREATE INDEX IX_Employees_Department_LastName
ON Employees(Department, LastName);
```

This index would be useful for queries that filter by:
- Department alone
- Department and LastName together
- But not for queries filtering only by LastName

## Covering Indexes

A covering index includes all columns referenced in a query, eliminating the need to access the table itself.

### Benefits:
- Significantly improves performance by avoiding table lookups
- Reduces I/O operations
- Often created as composite indexes with INCLUDE columns

### Example:
```sql
CREATE INDEX IX_Orders_CustomerID_OrderDate
INCLUDE (TotalAmount, Status)
ON Orders(CustomerID, OrderDate);
```

## Filtered Indexes

Filtered indexes include only a subset of rows that match a specific condition.

### Advantages:
- Smaller size than full-table indexes
- More efficient maintenance
- Better statistics for specific subsets of data

### Example:
```sql
CREATE INDEX IX_Orders_Status
ON Orders(Status)
WHERE Status = 'Active';
```

## Columnstore Indexes

Columnstore indexes store and process data by columns rather than rows, designed for analytical workloads.

### Key features:
- High compression rates
- Exceptional performance for aggregate queries
- Ideal for data warehousing and analytical processing
- Available as both clustered and non-clustered variants

## Spatial Indexes

Specialized indexes for spatial data types that enable efficient queries on geographical information.

### Used for:
- Proximity queries
- Containment queries
- Intersection queries

## Full-text Indexes

Designed for text search operations on character-based data.

### Capabilities:
- Word and phrase searches
- Linguistic matching
- Relevance ranking
- Support for different languages

## XML Indexes

Specialized indexes for XML data to support efficient XQuery and XPath operations.

### Types:
- Primary XML indexes
- Secondary XML indexes (PATH, VALUE, PROPERTY)

## Hash Indexes

Available in memory-optimized tables, hash indexes provide direct key-to-row lookups.

### Characteristics:
- Very fast point lookups
- Fixed size determined at creation
- Not suitable for range scans

## Considerations for Index Selection

- Query patterns (filtering, sorting, joining)
- Column data distribution
- Update frequency
- Storage requirements
- Performance requirements

Proper index selection is critical for database performance optimization.