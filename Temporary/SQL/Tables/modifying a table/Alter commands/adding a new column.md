to add a new column to our already exists table using alter we use this syntax

#  Syntax

```SQL
ALTER TABLE table_name
ADD column_name data_type;
```

## Examples

### Adding a Simple Column

This adds a new column `age` of type `INT` to the `users` table.

```sql
ALTER TABLE users
ADD age INT;
```

### Adding a Column with a `DEFAULT` Value

You can specify a default value for the new column. Existing rows will get this default value.

```sql
ALTER TABLE products
ADD stock_quantity INT DEFAULT 0;
```

### Adding a Column with `NOT NULL` Constraint

If you add a `NOT NULL` column to a table that already contains data, you **must** also provide a `DEFAULT` value. Otherwise, the operation will fail because existing rows would have `NULL` for the new column, violating the `NOT NULL` constraint.

```sql
-- This will fail if 'employees' table already has rows, as 'email' would be NULL
-- ALTER TABLE employees
-- ADD email VARCHAR(255) NOT NULL;

-- Correct way: Add NOT NULL with a DEFAULT value
ALTER TABLE employees
ADD email VARCHAR(255) NOT NULL DEFAULT 'no_email@example.com';
```

### Adding a Column with a `UNIQUE` Constraint

```sql
ALTER TABLE users
ADD username VARCHAR(50) UNIQUE;
```

### Adding a Column at a Specific Position

You can use `FIRST` to add the column as the first column, or `AFTER existing_column_name` to place it after a specific column.

```sql
-- Add 'id' as the first column
ALTER TABLE new_table
ADD id INT FIRST;

-- Add 'middle_name' after 'first_name'
ALTER TABLE employees
ADD middle_name VARCHAR(50) AFTER first_name;
```

### Adding Multiple Columns

You can add several columns in a single `ALTER TABLE` statement.

```sql
ALTER TABLE orders
ADD COLUMN order_date DATE,
ADD COLUMN total_amount DECIMAL(10,2) DEFAULT 0.00;
```

- **NOTE**: When adding a `NOT NULL` column to an existing table, always remember to provide a `DEFAULT` value to avoid errors for existing rows.

