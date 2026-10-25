is a function to check whether a variable has been not declared or if it has a default value

# Syntax

```Php
$returnVariable = empty($variable)
```

it will return true if a variable has not declared or if it has a default value:

- The variable **doesn't exist** (i.e., it hasn't been declared).
- The variable has been assigned the value **`NULL`**.
- The variable is a boolean and its value is **`false`**.
- The variable is an integer or float and its value is **`0`** or **`0.0`**.
- The variable is a string and its value is an **empty string (`""`)** or the string **`"0"`**.
- The variable is an **empty array** (`array()`).
- The variable is a property of an object that is only declared but has not been assigned a value.

otherwise it will return false

```Php
<?php
$a = 0;
$b = "";
$c = "Hello";
$d = array();
// $e is not set

var_dump(empty($a)); // true (because $a is 0)
var_dump(empty($b)); // true (because $b is an empty string)
var_dump(empty($c)); // false (because $c is "Hello")
var_dump(empty($d)); // true (because $d is an empty array)
var_dump(empty($e)); // true (because $e is not defined)
var_dump(empty("0")); // true (because "0" is an empty-like string)
?>
```