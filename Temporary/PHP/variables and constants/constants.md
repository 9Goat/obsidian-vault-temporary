just like other programming languages you can set up constant variables that cannot change their values after declaration

# Syntax

```Php
define("constantName",value);
//OR
const constantName = value;

//to access a constant you dont need to use the dollar sign ($), you can simply use the constant name.

echo constantName;
```

# defined

defined is used to check whether a constant variable exists or not.and it will return either true or false

## Example

```Php
<?php
define("MY_CONSTANT", "Hello");

if (defined("MY_CONSTANT")) {
    echo "MY_CONSTANT is defined and its value is: " . MY_CONSTANT;
} else {
    echo "MY_CONSTANT is not defined.";
}

echo "\n";

if (defined("ANOTHER_CONSTANT")) {
    echo "ANOTHER_CONSTANT is defined.";
} else {
    echo "ANOTHER_CONSTANT is not defined.";
}
?>
```

# Example

```Php
<?php

define("constant1", "this is a constant");
echo constant1;

echo "<br>";

const constant2 = "this is another constant";
echo constant2;

?>
```
# Notes

- you cannot declared a constant variable without initialising it
- you cannot change the value of a constant
- the `defined` method only works on constants not variables (*use isset instead*)