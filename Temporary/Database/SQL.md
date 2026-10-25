# LDD

##  CREATE TABLE

**Basic syntax**

```SQL
create table table_name{
attribute_name datatype column_constraint,
attribute_name2 datatype column_constraint,
...
}
```

### Datatypes

- **char(n)**: stores n characters with a fixed length  meaning if we insert "Hi" into char(5) the result will be `Hi     ` with 5 trailing spaces
- **Varchar(n):** very similar to char except that it only stores the length of the actual string. + a single byte for the length of the string.
- **integer or int**: is used to store whole numbers (numbers without decimal points) 
- **number and decimal for floating numbers**: decimal (5,2) Allows numbers like 123.45 (max value 999.99)
	- **Syntax:** `DECIMAL(P, S)` or `NUMERIC(P, S)`
		- **P (Precision):** The total number of digits that can be stored (both before and after the decimal point).
		- **S (Scale):** The number of digits to the right of the decimal point.
- **number for whole numbers** if we dont specify the precision we can use number as an alternative to integer to store whole numbers. For example number(3) will allow use to store a maximum of 999
- **date** allows us to store dates (YYYY-MM-DD HH:MM:SS)

### column constraints
#### Order

| **Order** | **Constraint Type**  | **Keyword / Syntax**         | **Description**                                                                           |
| --------- | -------------------- | ---------------------------- | ----------------------------------------------------------------------------------------- |
| **1.**    | **Data Type**        | `INT`, `VARCHAR(50)`, `DATE` | _Always first._ Defines the type and size of the data.                                    |
| **2.**    | **Nullability**      | `NOT NULL` or `NULL`         | Defines whether the column can contain empty/undefined values.                            |
| **3.**    | **Default Value**    | `DEFAULT value`              | Defines the value inserted if the user omits the column in an `INSERT` statement.         |
| **4.**    | **Uniqueness Check** | `UNIQUE`                     | Ensures that every value in the column is different (allows NULLs, unlike `PRIMARY KEY`). |
| **5.**    | **Domain Check**     | `CHECK (condition)`          | Ensures the value meets a custom logical condition (e.g., a score is between 1 and 10).   |
| **6.**    | **Primary Key**      | `PRIMARY KEY`                | Defines the column as the table's main identifier (enforces `NOT NULL` and `UNIQUE`).     |
| **7.**    | **Foreign Key**      | `REFERENCES Table (Column)`  | Defines the column as referencing a primary or unique key in another table.               |
#### Example

```SQL
CREATE TABLE Employees (
    employee_id     INT PRIMARY KEY,
    department_fk   TINYINT
                    -- 1. NOT NULL partment)
                    NOT NULL
                    -- 2. DEFAULT
                    DEFAULT 10
                    -- 3. UNIQUE
                    UNIQUE
                    -- 4. CHECK 
                    CHECK (department_fk BETWEEN 10 AND 99)
                    -- 5. FOREIGN KEY
                    REFERENCES Departments (department_id) 
);
```

#### Notes

if a table contains multiple foreign keys or primary keys we **HAVE** to write them as table constraints not inline column constraints

### Table constraints

#### Syntax

``` SQL
CONSTRAINT constraint_name constrain
```

| **Constraint Type** | **Keyword**                                       | **Purpose**                                                                                                                                      |
| ------------------- | ------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Primary Key**     | `PRIMARY KEY (col1, col2, ...)`                   | Defines the unique identifier for the table. **Mandatory** when the key is **composite** (made of 2+ columns).                                   |
| **Foreign Key**     | `FOREIGN KEY (col_set) REFERENCES Table(col_set)` | Enforces **Referential Integrity** by linking columns in this table to a Primary/Unique Key in another table.                                    |
| **Unique**          | `UNIQUE (col1, col2, ...)`                        | Ensures that the combination of values in the specified columns is unique across the entire table.                                               |
| **Check**           | `CHECK (condition)`                               | Enforces a condition that must be true for _every_ row in the table, often involving a comparison between two different columns in the same row. |

#### Examples

```SQL
CREATE TABLE Payment (
    payment_id  INT PRIMARY KEY,
    amount      DECIMAL(10, 2),
    fee         DECIMAL(10, 2),

    -- Ensures the fee is never more than 10% of the total payment amount
    CONSTRAINT CK_FeeLimit CHECK (fee <= amount * 0.10) 
);
```

### on delete foreign keys

at then end of the foreign key can we set the behavior of what will happens  if a foreign key  gets deleted

|**Action**|**When Customer is Deleted**|
|---|---|
|`ON DELETE RESTRICT`|Fails. (Orders remain)|
|`ON DELETE CASCADE`|Orders are automatically deleted.|
|`ON DELETE SET NULL`|Order's `customer_id` is set to NULL.|
|`ON DELETE SET DEFAULT`|Order's `customer_id` is set to the column's default value (if one exists).|

## ALTER TABLE

### add column

#### Syntax

```SQL
ALTER TABLE table_name
ADD COLUMN column_name data_type [column_constraints];
```

#### Example

```SQL
ALTER TABLE Employees
ADD COLUMN email VARCHAR(255) UNIQUE;
```

### drop column

#### Syntax

```SQL
ALTER TABLE table_name
DROP COLUMN column_name;
```

#### Example

```SQL
ALTER TABLE Employees
DROP COLUMN old_phone_number;
```

### modify column

#### Syntax

```SQL
ALTER TABLE table_name
MODIFY column_name new_data_type [new_constraints];
```

#### Example

```SQL
ALTER TABLE Employees
MODIFY last_name VARCHAR(100) NOT NULL;
```

### add constraint

#### Syntax

```SQL
ALTER TABLE table_name
ADD CONSTRAINT constraint_name PRIMARY KEY (column_list);
```

#### Example

```SQL
ALTER TABLE Orders
ADD CONSTRAINT FK_EmployeeOrder
FOREIGN KEY (employee_id) REFERENCES Employees (employee_id)
ON DELETE SET NULL;
```

### drop constraint

#### Syntax

```SQL
ALTER TABLE table_name
DROP CONSTRAINT constraint_name;
```

#### Example

```SQL
ALTER TABLE Loan
DROP CONSTRAINT CK_DateOrder;
```

## Drop table

### Syntax

```SQL
drop table table_name
```

### Example

```SQL
drop table customers
```

# LMD

## insert into

### Syntax

```SQL
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);

OR

INSERT INTO table_name
VALUES (value1, value2, value3, ...);
```

- when we dont specify the columns we instead **HAVE** to provide values for all the columns
- also the values must match the columns in datatypes and order to be a valid insert

### Examples

```SQL
INSERT INTO Orders (order_id, customer_id, order_date)
VALUES (1001, 55, '2025-12-10');
```

```SQL
INSERT INTO Orders
VALUES (1002, 56, '2025-12-11', 150.50, '123 Main St');
```

### insert with select from an another table

```SQL
INSERT INTO target_table (column1, column2, ...)
SELECT column_A, column_B, ...
FROM source_table
WHERE condition;
```

- this insert into requires 2 tables to be valid

#### Example

```SQL
INSERT INTO Orders_Archive (order_id, customer_id, order_date)
SELECT order_id, customer_id, order_date
FROM Orders
WHERE order_date < '2025-01-01';
```

## update set

```SQL
UPDATE table_name
SET column1 = new_value1, column2 = new_value2, ...
WHERE condition;
```

### Conditions

#### 1. Comparison Operators

These are used to compare two values (a column value, a literal value, or the result of an expression).

|Operator|Meaning|Example|
|---|---|---|
|`=`|Equal to|`salary = 50000`|
|`<`|Less than|`age < 18`|
|`>`|Greater than|`quantity > 10`|
|`!=` or `<>`|Not equal to|`status <> 'Complete'`|
|`<=`|Less than or equal to|`price <= 10.99`|
|`>=`|Greater than or equal to|`order_date >= '2025-12-01'`|

#### 2. Logical Operators

These are used to combine multiple simple conditions into a single, complex condition.

|Operator|Meaning|Example|
|---|---|---|
|**AND**|Both conditions must be true|`age >= 18 AND status = 'Active'`|
|**OR**|At least one condition must be true|`department = 'Sales' OR department = 'Marketing'`|
|**NOT**|Negates the following condition|`NOT (country = 'USA')`|

#### 3. Special Predicates (Advanced Operators)

These are unique operators used for specific, common filtering needs.

|Predicate|Meaning|Example|
|---|---|---|
|**BETWEEN**|Checks if a value is within a specified range (inclusive).|`price BETWEEN 10 AND 50` (Equivalent to `price >= 10 AND price <= 50`)|
|**IN**|Checks if a value matches any value in a list of values.|`state IN ('NY', 'CA', 'TX')`|
|**LIKE**|Searches for a pattern in a string. Uses wildcards: `%` (any number of characters) and `_` (exactly one character).|`last_name LIKE 'Smi%'`|
|**IS NULL**|Checks for a missing or undefined value.|`manager_id IS NULL`|
|**IS NOT NULL**|Checks for a defined value.|`email IS NOT NULL`|
|**EXISTS**|Checks for the existence of any rows returned by a subquery. (Returns TRUE if the subquery returns at least one row.)|`EXISTS (SELECT 1 FROM Orders WHERE Orders.customer_id = Customers.id)`|
|**ANY / ALL**|Used with comparison operators to compare a value against a set of values returned by a subquery.|`salary > ALL (SELECT salary FROM Employees WHERE department = 'Sales')`|
##### Example

```SQL
SELECT employee_name, hire_date, salary
FROM Employees
WHERE 
    -- Condition 1: Employees hired in 2024
    (hire_date BETWEEN '2024-01-01' AND '2024-12-31') 
    
    -- Condition 2: AND belong to one of these two departments
    AND department_id IN (10, 20)
    
    -- Condition 3: AND their salary is NOT null
    AND salary IS NOT NULL;
```
### Example

```SQL
UPDATE Employees
SET email = 'new.user@company.com'
WHERE employee_id = 105;
```

### Note

- if you omit the where clause it will update all the rows in the table instead

## delete from

### Syntax

```SQL
DELETE FROM table_name
WHERE condition;
```

### Example

```SQL
DELETE FROM Orders
WHERE order_id = 2001;
```

# LID

## Syntax and order

```SQL
-- 5. SELECT (Projection and Aggregation)
SELECT 
    column_name_1, 
    aggregate_function(column_name_2),
    ...
FROM 
    table_name  -- 1. FROM (Source)
WHERE 
    condition_on_individual_rows  -- 2. WHERE (Row Filter)
GROUP BY 
    column_name_1, 
    column_name_3, 
    ...  -- 3. GROUP BY (Grouping criteria: non-aggregated columns from SELECT must be here)
HAVING 
    condition_on_aggregated_groups  -- 4. HAVING (Group Filter, usually uses aggregate functions)
ORDER BY 
    column_name_4 [ASC | DESC];  -- 6. ORDER BY (Sorting the final result set)
```



## Basic select

### Syntax

```SQL
SELECT column1, column2, ...
FROM table_name
WHERE condition_that_must_be_true;
```

### Example

```SQL
SELECT Name, Salary
FROM Employee
WHERE Department = 'Sales'          -- Selection Condition 1
  AND Salary < 60000;               -- Selection Condition 2
```

## Aggregate functions

| **Function** | **Purpose**                                    | **Example**          |
| ------------ | ---------------------------------------------- | -------------------- |
| **COUNT()**  | Counts the number of rows/values in the group. | `COUNT(employee_id)` |
| **SUM()**    | Calculates the total sum of the column values. | `SUM(order_total)`   |
| **AVG()**    | Calculates the average value of the column.    | `AVG(salary)`        |
| **MIN()**    | Finds the minimum value in the group.          | `MIN(hire_date)`     |
| **MAX()**    | Finds the maximum value in the group.          | `MAX(salary)`        |

## group by +  having

group by is used to group rows that have the same values into a single row representing that value

- **Rule:** Any column listed in the `SELECT` clause that is **not** inside an aggregate function **must** also be listed in the `GROUP BY` clause.

having is used to filter grouped rows meaning we *mostly* use it with exaggerate functions.But it can also use regular rows for filtering which makes is just a second version of where

### Examples

```SQL
SELECT
    Department,
    COUNT(employee_id) AS EmployeeCount
FROM
    Employees
GROUP BY
    Department
HAVING
    COUNT(employee_id) > 10;  -- Filtering groups that have more than 10 employees
```

```SQL
SELECT
    Department,                    -- 1. Show the name of the group
    SUM(Salary) AS Total_Payroll   -- 2. Calculate the sum of salaries for each group
FROM
    Employee
WHERE
    Department <> 'Marketing'      -- 3. (Optional) Filter out the Marketing dept first (row filtering)
GROUP BY
    Department                     -- 4. Group remaining rows by Department
HAVING
    SUM(Salary) > 150000           -- 5. Filter the groups: only keep groups where Total_Payroll > 150000
```

## order by

### A. Direction Keywords

You must specify the sorting direction using one of these keywords:

- **`ASC` (Ascending):** Sorts the data from lowest to highest (A to Z, 0 to 9, oldest date to newest date). This is the **default** behavior if no keyword is specified.
- **`DESC` (Descending):** Sorts the data from highest to lowest (Z to A, 9 to 0, newest date to oldest date)
### B. Sorting Hierarchy

You can sort by multiple columns, which defines a sorting hierarchy:

- The data is sorted first by the **first** column listed.
- If two or more rows have the same value in the first column, they are then sorted by the **second** column listed, and so on.

### Examples

```SQL
SELECT name, salary
FROM Employees
ORDER BY salary DESC;
```

```SQL
SELECT product_name, category, price
FROM Products
ORDER BY category ASC, price DESC;
```

## joins

joins are used to group multiple tables together in the from phase

![[image-143.png]]

### inner join

The `INNER JOIN` (often just called `JOIN`) is used to retrieve rows from **two or more tables** that have matching values in a specified column or columns.

#### Examples

```SQL
SELECT
    C.Name,
    O.OrderID
FROM
    Customers AS C
INNER JOIN
    Orders AS O
ON
    C.CustomerID = O.CustomerID; -- The join condition
```

![[image-144.png]]

### Natural join

![[image-145.png]]



| Feature                 | Natural Join                                                    | Inner Join                                                              |
| ----------------------- | --------------------------------------------------------------- | ----------------------------------------------------------------------- |
| Join Condition          | Automatically matches columns with the same name and data type  | Requires explicit join condition using ON clause                        |
| Common Columns          | Includes only one copy of each common column                    | Includes both copies, which can lead to duplicate column names          |
| Syntax Simplicity       | Shorter and simpler (no need to write the join condition)       | More flexible but needs join condition to be defined                    |
| Control Over Join Logic | Less control (relies on column names being the same)            | Full control over how tables are joined                                 |
| Use Case                | When tables share common column names and you want a quick join | When you want to join on specific columns or use different column names |

#### Examples

![[image-148.png]]![[image-149.png]]![[image-150.png]]

as we can see it combines the rows containing the same information (it basically automatically performs on e.dept_name = d.dept_name)

### Outer joins

outer joins are basially inner joins plus that if a row in one table does not have a match in the other table, the result will still include that row, with NULL values for the columns from the other table.

#### left

includes all the rows from the left table

![[image-151.png]]

#### right

includes all the rows from the right table

![[image-152.png]]

#### full

a combination of both right and left

![[image-153.png]]

### Cross join

returns the resulting of multiplying the tables with each other meaning if we get a table with 4 rows and a table with 3 rows the cross join will contain 12 rows.cross join also takes no condition

```SQL
select columns from table1 cross join table2
```

#### Examples

![[image-154.png]]

## Subqueries

A subquery is a query nested inside another query. subqueries are found inside of where and having

### Example

```SQL
SELECT
    Emp_ID,
    Salary
FROM
    Employees
WHERE
    Salary > (
        -- Subquery (Inner Query): Calculates the single value needed for comparison
        SELECT AVG(Salary)
        FROM Employees
    );
```

## Set Operations

![[image-159.png]]

Set operations are used to combine the results of two or more SELECT statements into a single result set. The main set operations are UNION, INTERSECT, and Minus.Also the selected columns from both tables must be the same

1. **Different Number of Columns:** The two `SELECT` statements must return the **exact same count** of columns (attributes).
2. **Incompatible Data Types:** The columns in the first position of both queries must have compatible data types, the columns in the second position must have compatible types, and so on.

### UNION

The `UNION` operator combines the result sets of two or more `SELECT` statements into a single result set.

The result set contains all distinct (unique) rows from the first query **PLUS** all distinct rows from the second query.

- **`UNION` (default):** Automatically removes duplicate rows.
- **`UNION ALL`:** Keeps all rows, including duplicates. (Faster, as it skips the de-duplication step).

**The Rule**

The column names of the final result set are determined **only** by the first query. Any column names or aliases defined in the second query are ignored.

#### Example


![[image-155.png]]

### INTERSECT

The `INTERSECT` operator returns the rows that are common to **both** the first and second query result sets.

![[image-157.png]]

in this example we selected name from both queries

### minus

returns the rows that are present in the **first query's result set** but **NOT** in the second query's result set.

#### Example

![[image-158.png]]