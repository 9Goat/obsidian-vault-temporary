to use a database we use the command **`USE`** followed by the name of the database

# Syntax

```SQL
USE database_name;
```

- this command is best paired with [[Selecting current database]] to see if the command execution was successful

# Example

```SQL
USE TechZone; # using a database that is called TechZone
SELECT DATABASE(); # showcasing the currently used database
```


## Result

![[image-215.png]]


# How to UNUSE a database

lets say that we dont want to be associated with any database anymore, the way to do this is to create a temporary database ,use it with the use function and then drop that database so the system pushes it back into *null* database

## Syntax

```SQL
CREATE DATABASE temp_unuse;
USE temp_unuse;
DROP DATABASE temp_unuse;

SELECT DATABASE(); -- This will now return NULL
```

