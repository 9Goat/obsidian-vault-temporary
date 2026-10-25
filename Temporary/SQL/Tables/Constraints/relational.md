
the referential integrity category contains the `FOREIGN KEY` constraint.

# FOREIGN KEY

The Foreign Key acts as a "bridge" between two tables, establishing a link based on common column(s). It ensures that relationships between tables are valid and maintained, preventing actions that would destroy links between data.

- **Rules:**
    - A Foreign Key column(s) in the child table must reference a `PRIMARY KEY` or `UNIQUE` key in the parent table.
    - The data types of the Foreign Key column(s) must match the data types of the referenced column(s).
    - A Foreign Key column **can** contain `NULL` values, unless it is also defined as `NOT NULL`.
    - When a row in the parent table is deleted or updated, the Foreign Key defines the action to take on related rows in the child table (e.g., `CASCADE`, `SET NULL`, `RESTRICT`).

## Example (Column Level)

This method defines the foreign key directly after the column definition.

```SQL
CREATE TABLE departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(100) NOT NULL
);

CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    department_id INT REFERENCES departments(department_id)
);
```

## Example (Table Level)

Defining the foreign key at the table level allows for naming the constraint and specifying actions for `ON DELETE` and `ON UPDATE`. This is generally preferred for clarity and flexibility.

```SQL
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    customer_name VARCHAR(100)
);

CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    order_date DATE,
    CONSTRAINT fk_customer_id
        FOREIGN KEY (customer_id)
        REFERENCES customers(customer_id)
        ON DELETE CASCADE
        ON UPDATE RESTRICT
);
```

### Actions on Referential Integrity

When a row in the parent table (the one with the `PRIMARY KEY` or `UNIQUE` key) is deleted or updated, the `FOREIGN KEY` constraint can specify how the database should react to the related rows in the child table.

|**Action**|**Description**|
|---|---|
|`ON DELETE CASCADE`|If a row in the parent table is deleted, all corresponding rows in the child table are also deleted.|
|`ON UPDATE CASCADE`|If a referenced key in the parent table is updated, the foreign key values in the child table are also updated.|
|`ON DELETE SET NULL`|If a row in the parent table is deleted, the foreign key column(s) in the child table are set to `NULL`. (Requires the foreign key column(s) to be nullable).|
|`ON UPDATE SET NULL`|If a referenced key in the parent table is updated, the foreign key values in the child table are set to `NULL`. (Requires the foreign key column(s) to be nullable).|
|`ON DELETE RESTRICT`|Prevents the deletion of a row in the parent table if there are any referencing child rows. This is often the default behavior.|
|`ON UPDATE RESTRICT`|Prevents the update of a referenced key in the parent table if there are any referencing child rows. This is often the default behavior.|
|`ON DELETE NO ACTION`|Similar to `RESTRICT` in MySQL; the deletion is rejected if there are related child rows.|
|`ON UPDATE NO ACTION`|Similar to `RESTRICT` in MySQL; the update is rejected if there are related child rows.|

## Disabling Foreign Key Checks (MySQL Specific)

In MySQL, you can temporarily disable foreign key checks. This can be useful for operations like importing data where the order of insertion might violate constraints temporarily, or when dropping and recreating tables.

```sql
-- Disable foreign key checks
SET FOREIGN_KEY_CHECKS = 0;

-- Perform operations that might temporarily violate foreign key constraints
-- e.g., INSERT, UPDATE, DELETE, DROP TABLE, CREATE TABLE

-- Re-enable foreign key checks
SET FOREIGN_KEY_CHECKS = 1;
```

- **NOTE**: Always remember to re-enable `FOREIGN_KEY_CHECKS` after your operations are complete to maintain data integrity.

