the uniqueness category contains 2 main constraints which are:

- Unique
- Primary key

# UNIQUE

he Unique constraint ensures all values in a column are different from one another.

## Example

```SQL
-- Column Level
CREATE TABLE users (
    id INT PRIMARY KEY,
    email VARCHAR(255) UNIQUE
);

-- Table Level
CREATE TABLE users (
    id INT PRIMARY KEY,
    email VARCHAR(255),
    CONSTRAINT uq_user_email UNIQUE (email)
);
```

# PRIMARY KEY

The Primary Key is the "ID card" of your table. It uniquely identifies every single row.

- **Rules:** It must be unique, and it **cannot** contain `NULL` values.
- **Limit:** A table can have only **one** Primary Key.

## Example

```SQL
-- Column Level (Simple)
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100)
);

-- Table Level (Better for naming or composite keys)
CREATE TABLE employees (
    employee_id INT,
    name VARCHAR(100),
    CONSTRAINT pk_employee_id PRIMARY KEY (employee_id)
);
```

- **NOTE**: a **`PRIMARY KEY`** can consist of more than a single column from the table (we call this *composite primary key* )

```SQL
CREATE TABLE classroom_assignments (
    student_id INT,
    room_id INT,
    assignment_date DATE,
    -- This MUST be at the table level
    PRIMARY KEY (student_id, room_id)
);
```

|**Feature**|**Single Primary Key**|**Composite Primary Key**|
|---|---|---|
|**Definition**|Column or Table Level|**Table Level Only**|
|**Columns**|Exactly one|Two or more|
|**Identification**|One ID (e.g., `user_id`)|A relationship (e.g., `order_id` + `product_id`)|
|**Nullability**|Never allowed|None of the columns in the key can be NULL|

