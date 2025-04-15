# Identity Property in SQL Server Columns

An identity property in SQL Server is a column attribute that automatically generates sequential numeric values when new rows are inserted. It's commonly used for primary key columns.

## Key Characteristics

- **Auto-incrementing**: Values are generated automatically by the database
- **Not updatable**: Cannot be manually modified once set
- **Uniqueness**: Guarantees unique values for each row
- **Configuration**: Defined by seed (starting value) and increment

## Syntax

When creating a table:
```sql
CREATE TABLE Employees (
    EmployeeID INT IDENTITY(1,1) PRIMARY KEY,
    Name VARCHAR(100)
)
```

The `IDENTITY(1,1)` means:
- Start at 1 (seed)
- Increment by 1 for each new row

## Common Operations

**Check if a column has identity property:**
```sql
SELECT 
    COLUMNPROPERTY(OBJECT_ID('TableName'), 'ColumnName', 'IsIdentity')
```

**Get current identity value:**
```sql
SELECT IDENT_CURRENT('TableName')
```

**Reset identity value:**
```sql
DBCC CHECKIDENT ('TableName', RESEED, NewValue)
```

**Insert with explicit identity values:**
```sql
SET IDENTITY_INSERT TableName ON
-- Insert statements with explicit values
SET IDENTITY_INSERT TableName OFF
```

Identity properties simplify primary key management but can sometimes cause issues with data migration or when you need more control over key generation.