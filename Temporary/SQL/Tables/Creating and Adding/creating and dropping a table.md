# Creating a table

here is the syntax for creating a database, the following syntax will only show the basic create function for other complex statements like constraint the will contain their own notes

## Syntax

```SQL
CREATE TABLE [IF NOT EXISTS] table_name(
   column1 datatype constraints,
   column2 datatype constraints,
   ...
);
```

- `IF NOT EXISTS` checks if the table name exists if it does, the table won't be created, thus preventing errors from occurring due to attempting to create a table with a name that is already in use. 
- `table_name`: This is the name of the table that you want to create.
- `column1`, `column2`, etc.: The names of the columns in the table.
- `datatype`: the data of each column such as `INT`, `VARCHAR`, `DATE`, etc.
- `constraints`: These are optional constraints such as `NOT NULL`, `UNIQUE`, `PRIMARY KEY`, and `FOREIGN KEY`.

## Example

```SQL
CREATE DATABASE example_db;
USE example_db;

CREATE TABLE users (
id INT AUTO_INCREMENT PRIMARY KEY,
username VARCHAR(50) NOT NULL UNIQUE,
email VARCHAR(100) NOT NULL UNIQUE,
created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

# Dropping a table

to drop a table we must first be inside the database containing that table so we use the command [[Using a database|use]] ,followed by the following command from this syntax

## Syntax

```SQL
DROP TABLE [IF EXISTS] table_name;
```

##  Example

after we have created the users table our  objective now is to drop it using this command

```SQL
USE example_db;

DROP TABLE IF EXISTS users;
```

![[image-218.png]]

