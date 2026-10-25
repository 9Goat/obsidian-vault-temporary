# Loading the driver

before connecting to our database we need to load the driver to our database

```java
try {
Class.forName("com.mysql.cj.jdbc.Driver");
System.out.println("Driver OK!!!");
} 
catch (ClassNotFoundException e) {
System.err.println("problème de chargement du driver "+e.getMessage());
System.exit(1);
}
```

- the drive link differs depending on the type of DBMS we are using

# Connecting to the database

## Define the connection settings

before we connect to the database we need to define the connection variables that will hold the database information

```java
Connection con=null;
String url="jdbc:mysql://localhost:3306/stockdb";
String user="root";
String password="";
```

- the end of the url contains the name of the database

## connecting

```java
try {
con=DriverManager.getConnection(url, user,password);
System.out.println("connection ok!!!");
}
catch (SQLException e) {
System.err.println("Error opening SQL connection:"+e.getMessage());
}
```

## Important

remember to always close the connection with database with `con.close()` at the end of our code

# Queries

there are 2 types of queries that we will be working with, which are the following :

- **executeQuery**: works for `SELECT` operations
	- **Syntax**: `Statement.executeQuery().`
	- **Result**:  returns the selected rows as a **`java.sql.ResultSet`** value
- **executeUpdate**: works for `INSERT, UPDATE, DELETE, CREATE TABLE and DROP TABLE`
	- **Syntax**: `Statement.executeUpdate()`
	- **Result**: returns the number of rows affected by this query

- in our case the **`Statement`** variable will be replaced with our statements variable (see below)

## Working with ResultSet

when working with select query we store the result inside the ResetSet variable,

### Declaration

```java
ResultSet rs = null;
```

### iterating over elements

to iterate over the ResultSet we use a while loop with the `.next()` method that returns a boolean

```java
rs = stmt.executeQuery(sql);

while (rs.next()) {
    //statments go here
}
```

### accessing the data in a **ResultSet**

to access the elements of the ResultSet inside the  while loop we use one of the following methods, depending on the database of the element we want to access

|**Java Data Type**|**ResultSet Method**|**Example**|
|---|---|---|
|`int` / `Integer`|`rs.getInt("column_name")`|`int age = rs.getInt("age");`|
|`String`|`rs.getString("column_name")`|`String email = rs.getString("email");`|
|`double`|`rs.getDouble("column_name")`|`double salary = rs.getDouble("salary");`|
|`boolean`|`rs.getBoolean("column_name")`|`boolean active = rs.getBoolean("is_active");`|
|`LocalDate` / `Date`|`rs.getDate("column_name")`|`Date joined = rs.getDate("join_date");`|

- we can also access elements by their index not just their column names, here is an example
	- **Example**: 

```java
// If query is: SELECT id, first_name FROM users
int id = rs.getInt(1);         // Grabs 'id'
String name = rs.getString(2); // Grabs 'first_name'
```

- at the end of executing a query with `ResultSet` we have to close it with `.close()`
# statements

there are 2 types of statements that we will be discussing in this section which are the following:

- **statements**: which uses normal sql
- **prepared statements**: which use placeholders (`?`) for parameters and then fills those place holders with variables from our program

## Statements

### Creating the statements

before we start executing queries to we need to create the statement

```java
Statement stmt = null;
try {
stmt = conn.createStatement();
}
catch (SQLException e) {
System.err.println("Error creating SQL statement: "+e.getMessage());
}
```

- we dont have to create a new statement for every  query execution, we can always reuse the **`stmt`** variable whenever we want

### query execution

**Code example**

```java
Statement stmt = null;
ResultSet rs = null;
String sql = "SELECT id, name, price FROM products";

try {
    // Creating the statement
    stmt = con.createStatement();
    // Executing the query
    rs = stmt.executeQuery(sql);
    
    // Processing the result set
    while (rs.next()) {
        int id = rs.getInt("id");
        String name = rs.getString("name");
        double price = rs.getDouble("price");
        System.out.println("ID: " + id + ", Name: " + name + ", Price: " + price);
    }
} 
catch (SQLException e) {
    System.err.println("Error executing query: " + e.getMessage());
} 
```

##  Prepared statements

in the prepared statement there are 2 phases, which are:

- defining the prepared statement with `?` as place holders for variables
- executing the prepared statement by defining the variables for the placeholders

### Creating the prepared statement

this is the first phase

```java
String query = "INSERT INTO products (name, price, quantity) VALUES (?, ?, ?)";
PreparedStatement pstmt = null;

try {
    pstmt = con.prepareStatement(query);
} 
catch (SQLException e) {
    System.err.println("Error creating PreparedStatement: " + e.getMessage());
}
```

### query execution


```java
try {
    // 1. Set the values for the placeholders (1-indexed)
    pstmt.setString(1, "Gaming Mouse"); // replaces the 1st '?' (name)
    pstmt.setDouble(2, 29.99);          // replaces the 2nd '?' (price)
    pstmt.setInt(3, 50);                // replaces the 3rd '?' (quantity)

    // 2. Execute the statement
    int rowsInserted = pstmt.executeUpdate();
    System.out.println("Successfully inserted " + rowsInserted + " row(s)!");
} 
catch (SQLException e) {
    System.err.println("Error executing statement: " + e.getMessage());
} 
```

- to define the variables for the placeholders, we use their indexes and provide the value with `setDatatype(index,value)` the set methods use the same datatypes as the get methods in the `ResultSet`

## Important

- when we are done with our statement/ResultSet we need to close them after each query execution with `.close()`

# ResultSetMetaData

to get information about the `ResultSet` from our last query execution aka **SELECT** statement we use the `ResultSetMetaData`

## Declaring the ResultSetMetaData variable

```java
ResultSetMetaData metaData = null;
metaData = rs.getMetaData();
```

- `rs` is the variable of the ResultSet that we used after our latest query execution

##  Methods and informations

these are the methods and informations that we can get from the ResultSet metaData

- **`getColumnCount()`**
    - **Returns:** `int`
    - **Description:** Returns the total number of columns in the `ResultSet`.
- **`getColumnName(int column)`**
    - **Returns:** `String`
    - **Description:** Returns the actual name of the column in the database database table (e.g., `"user_id"`).
- **`getColumnType(int column)`**
	- **Returns:** `int`
	- **Description:** Returns the SQL data type as a constant integer defined in `java.sql.Types` (e.g., `Types.VARCHAR`, `Types.INTEGER`).
- **`getColumnTypeName(int column)`**
	- **Returns:** `String`
	- **Description:** Returns the database-specific type name (e.g., `"INT"`, `"VARCHAR"`, `"BLOB"`).
- **`isNullable(int column)`**
	- **Returns:** `int`
	- **Description:** Checks if a column can contain `NULL` values. It returns one of three constants:
	    - `ResultSetMetaData.columnNoNulls` (Cannot be null)
	    - `ResultSetMetaData.columnNullable` (Can be null)
	    - `ResultSetMetaData.columnNullableUnknown` (Unknown status)

- **Important** the parameter for all of these methods is the position of the column,(e.g., `1` for the first column).

## Code example

```java
// Assuming 'rs' is an active ResultSet
try {
    ResultSetMetaData rsmd = rs.getMetaData();
    int columnCount = rsmd.getColumnCount();
    
    System.out.println("Total Columns: " + columnCount);
    
    // Column index starts at 1
    for (int i = 1; i <= columnCount; i++) {
        System.out.println("Column " + i + ": " + rsmd.getColumnName(i) + " (" + rsmd.getColumnTypeName(i) + ")");
    }
} 
catch (SQLException e) {
    System.err.println("Metadata error: " + e.getMessage());
}
```

# DatabaseMetaData

while the `ResultSetMetaData` gathers information from an active ResultSet, `DatabaseMetaData` gathers information about the entire database

## Declaring the DatabaseMetaData variable

```java
DatabaseMetaData dbMeta = null;
dbMeta = conn.getMetaData();
```

## Methods and informations

these are the methods and informations that we can get from the connection metaData aka the entire database

- **`getTables()`**
	- **Returns:** `ResultSet`
	- **What it does:** Returns a list of all tables and views available in the entire database.
- **`getColumns()`**
	- **Returns:** `ResultSet`
	- **What it does:** Returns a massive map detailing every single column inside every table across the entire database.
- **`getPrimaryKeys()`**
	- **Returns:** `ResultSet`
	- **What it does:** Returns a list of all primary key configurations, showing which columns act as unique identifiers.
- **`getImportedKeys()`**
	- **Returns:** `ResultSet`
	- **What it does:** Returns a map of all Foreign Key relationships, showing how different tables link to one another.

### Parameters

here are they parameters that we need to pass to those methods to ensure they work properly

| **Method**        | **Param 1 (catalog)** | **Param 2 (schema)** | **Param 3 (tableName)** | **Param 4**                                                      |
| ----------------- | --------------------- | -------------------- | ----------------------- | ---------------------------------------------------------------- |
| `getTables`       | `null`                | `null`               | **`"%"`** _(All)_       | **`new String[]{"TABLE"}`** or null if we want to get everything |
| `getColumns`      | `null`                | `null`               | **`"YOUR_TABLE"`**      | **`"%"`** _(All columns)_                                        |
| `getPrimaryKeys`  | `null`                | `null`               | **`"YOUR_TABLE"`**      | _None_                                                           |
| `getImportedKeys` | `null`                | `null`               | **`"YOUR_TABLE"`**      | _None_                                                           |

## Code example

```java
// Assuming 'con' is an active Connection
try {
    DatabaseMetaData dbMeta = con.getMetaData();
    
    // 1. getTables() - List all tables in the database
    ResultSet tables = dbMeta.getTables(null, null, "%", new String[]{"TABLE"});
    System.out.println("--- Tables ---");
    while (tables.next()) {
        System.out.println("Table Name: " + tables.getString("TABLE_NAME"));
    }
    tables.close();
    
    // 2. getColumns() - List columns for the 'products' table
    ResultSet columns = dbMeta.getColumns(null, null, "products", "%");
    System.out.println("\n--- Columns in 'products' ---");
    while (columns.next()) {
        System.out.println("Column: " + columns.getString("COLUMN_NAME") + " (" + columns.getString("TYPE_NAME") + ")");
    }
    columns.close();
    
    // 3. getPrimaryKeys() - Get primary keys for 'products'
    ResultSet pks = dbMeta.getPrimaryKeys(null, null, "products");
    System.out.println("\n--- Primary Keys in 'products' ---");
    while (pks.next()) {
        System.out.println("PK Column: " + pks.getString("COLUMN_NAME"));
    }
    pks.close();
    
    // 4. getImportedKeys() - Get foreign keys for 'products'
    ResultSet fks = dbMeta.getImportedKeys(null, null, "products");
    System.out.println("\n--- Foreign Keys in 'products' ---");
    while (fks.next()) {
        System.out.println("FK Column: " + fks.getString("FKCOLUMN_NAME") + " -> References: " + fks.getString("PKTABLE_NAME"));
    }
    fks.close();

} 
catch (SQLException e) {
    System.err.println("Database metadata error: " + e.getMessage());
}
```