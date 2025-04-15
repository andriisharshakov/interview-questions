# Left Join in SQL

A left join returns all records from the left table and the matching records from the right table. If no match exists, NULL values are returned for all columns from the right table.

## Basic Syntax

```sql
SELECT columns
FROM Table1
LEFT JOIN Table2
ON Table1.column = Table2.column;
```

## Key Characteristics

- Returns all records from the left table
- Returns only matching records from the right table
- Uses NULL for right table columns when no match exists
- Also called LEFT OUTER JOIN (OUTER is optional)

## Example

```sql
SELECT c.CustomerName, o.OrderID, o.OrderDate
FROM Customers c
LEFT JOIN Orders o
ON c.CustomerID = o.CustomerID;
```

This query returns all customers and their orders, including customers who haven't placed any orders (their OrderID and OrderDate will be NULL).

## Common Use Cases

- Finding records in one table with no corresponding match in another
- Reporting that must include all records from a primary table
- Checking for "orphaned" or "missing" relationships

## Finding Unmatched Records

```sql
SELECT c.CustomerName
FROM Customers c
LEFT JOIN Orders o ON c.CustomerID = o.CustomerID
WHERE o.OrderID IS NULL;
```

This returns only customers who have never placed an order.

Left joins are excellent when you need all records from one table regardless of whether they have related records in another table.