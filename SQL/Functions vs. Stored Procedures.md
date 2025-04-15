# T-SQL: Functions vs. Stored Procedures

## Functions
- **Return values**: Must return a value (scalar or table)
- **Transactions**: Cannot start transactions
- **Usage**: Can be used in SELECT statements
- **DML operations**: Cannot perform INSERT, UPDATE, DELETE
- **Parameter direction**: Input parameters only
- **Error handling**: Limited error handling capabilities
- **Security**: Cannot use EXECUTE AS
- **Context**: Run in the calling statement's context

## Stored Procedures
- **Return values**: Optional return value, can return multiple result sets
- **Transactions**: Can control transactions
- **Usage**: Cannot be used in SELECT statements
- **DML operations**: Can perform all DML operations
- **Parameter direction**: Both input and output parameters
- **Error handling**: Full error handling with TRY/CATCH
- **Security**: Can use EXECUTE AS for security context
- **Context**: Run in their own execution context

## Performance Considerations
- Functions can cause performance issues when used in WHERE clauses on large tables
- Stored procedures benefit from execution plan caching
- Table-valued functions often perform worse than equivalent stored procedures

## When to Use Each
- **Use Functions when**: You need to encapsulate logic within a query
- **Use Stored Procedures when**: You need transactions, complex logic, or multiple operations

Functions are generally more restrictive but integrate better with queries, while stored procedures offer more power and flexibility for complex operations.