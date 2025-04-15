# Inner Join in SQL

An inner join combines rows from two or more tables based on a related column between them, returning only the rows where there's a match in both tables.

## Basic Syntax

```sql
SELECT columns
FROM Table1
INNER JOIN Table2
ON Table1.column = Table2.column;
```

## Key Characteristics

- Returns only matching records from both tables
- Discards rows that don't have corresponding matches
- Most common type of join operation
- The keyword "INNER" is optional (JOIN alone implies INNER JOIN)

## Example

```sql
SELECT o.OrderID, c.CustomerName, o.OrderDate
FROM Orders o
INNER JOIN Customers c
ON o.CustomerID = c.CustomerID;
```

This query returns all orders with their corresponding customer information, excluding any orders without matching customers and any customers without orders.

## Multiple Joins

```sql
SELECT o.OrderID, c.CustomerName, p.ProductName
FROM Orders o
INNER JOIN Customers c ON o.CustomerID = c.CustomerID
INNER JOIN OrderDetails od ON o.OrderID = od.OrderID
INNER JOIN Products p ON od.ProductID = p.ProductID;
```

Inner joins are ideal when you need data that requires valid relationships across all tables in your query.