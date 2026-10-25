in sql there are 3 categories of constraints which are the following:

- data checks
- uniqueness
- relational

in sql there are also 2 types of constraints which are :

- column constraints
- table constraints

**HERE IS A TABLE THAT SHOWS WHICH CONSTRAINTS CAN BE USED WITH WHICH TYPE**

| Constraint  | Column | Table |
| ----------- | ------ | ----- |
| CHECK       | Yes    | Yes   |
| NOT NULL    | Yes    | No*   |
| UNIQUE      | Yes    | Yes   |
| PRIMARY KEY | Yes    | Yes   |
| FOREIGN KEY | No     | Yes   |

# Column constraints

a column constraint is defined as part of the column definition meaning when we create a column we can insert a constraint definition directly into it. (this also applies when we use alter [[adding a new column]])

## Syntax 

```SQL
CREATE TABLE table_name (
. . .   
column_name datatype CONSTRAINT,
. . .);
```

## Example

```SQL
CREATE TABLE person ( 
. . .  
age INT CHECK (age >= 0),  
. . .);
```

- **NOTE**: it is not possible to have a column constraint with a constraint name like table constraint
# Table constraints

there are 2 ways to add a table constraint in SQL which are:

- when defining a table
- when using alter to define a constraint

## when defining a table

### Syntax

```SQL
CREATE TABLE table_name(
...
//columns here,
[CONSTRAINT constraint_name] constraint
)
```

- the `constraint` and `constraint_name` are both **OPTIONAL** meaning we can either have both of neither
- **NOTE**: the table constraint **MUST** be the final line in the table definition

### Examples

**EXAMPLE WITH A CONSTRAINT NAME**


```SQL
CREATE TABLE users (
id SERIAL PRIMARY KEY,
username VARCHAR(50) UNIQUE NOT NULL,
email VARCHAR(100) UNIQUE NOT NULL,
created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
CONSTRAINT email_format CHECK (email LIKE '%_@__%.__%')
);
```

**EXAMPLE WITHOUT A CONSTRAINT NAME**

```SQL
CREATE TABLE users (
id SERIAL PRIMARY KEY,
username VARCHAR(50) UNIQUE NOT NULL,
email VARCHAR(100) UNIQUE NOT NULL,
created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
CHECK (email LIKE '%_@__%.__%') #no name given
);
```

## when using alter

just like [[Introduction to constraint in mysql#when defining a table|when defining a table]] we can also add constraints with and without constraint names

### Syntax

```SQL
ALTER TABLE table_name ADD [CONSTRAINT constraint_name] consstraint;
```

- the `constraint` and `constraint_name` are both **OPTIONAL** meaning we can either have both of neither

### Examples


```SQL
-- Adding a NAMED constraint
ALTER TABLE products 
ADD CONSTRAINT uk_product_code UNIQUE (product_code);

-- Adding an UNNAMED constraint
ALTER TABLE products 
ADD UNIQUE (product_code);
```



