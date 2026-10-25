

the select statement can be used on databases to determine which database we are currently working with

#  Syntax

```SQL
SELECT DATABASE();
```

- **DATABASE()**  is a built in function that returns the name of the database we are currently working with

this query will return a single row with the name of the current database.

# Example

## when not logged on a database

it will simply just return NULL

![[image-213.png]]

## When logged onto a specific database

the `SELECT DATABASE()` query will return the name of the database that is currently in use.

```SQL
USE TechZone; //this statement will log us into a database called TechZone

SELECT DATABASE();
```

![[image-214.png]]



