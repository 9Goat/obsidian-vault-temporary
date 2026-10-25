just like other programming languages there are :function scope and global scope in Php

# Global

there are 2 main functionalities of **`global`** which are:

- making global variables accessible inside a certain function
- making a function scoped variable accessible outside of that function
	-  for this to work we need to first declare it using **`global`** **afterwards** in a new line inside the function we provide it with a value to make it global

# Example

```Php
$globalVar = "Hello, World!<br>";
function testFunction() {
    global $globalVar; // Accessing the global variable
    global $newVar;

    if (true) {
        $newVar = "This is a new variable.<br>"; //block scopes are also function scopes
    }
    echo $globalVar;
}
testFunction();
echo $newVar; // Accessing the new variable defined in the function

?>
```

# Notes

- there is **NO** block scope in php instead methods like if, for do not create a new scope, but their variables are accessible within the parent scope.

