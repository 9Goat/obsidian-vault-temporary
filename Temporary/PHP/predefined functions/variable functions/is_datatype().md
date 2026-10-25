this is not a single function but a collection of multiple functions we are going to discuss but i decided to group them together since they are very similar to each other

# Syntax

```Php
$returnVariable = is_datatype($variable); //will return a boolean
```

the supported datatypes for this function are:

- **is_array()**	Checks if the variable is an array.
- **is_bool()**	Checks if the variable is a boolean (true or false).
- **is_float()**	Checks if the variable is a floating-point number (decimal).
- **is_int()**	Checks if the variable is an integer (whole number).
- **is_object()**	Checks if the variable is an object.
- **is_string()**	Checks if the variable is a string.
- **is_callable()**	Checks if the variable's content can be called as a function (or method).
- **is_numeric()**	Checks if the variable is a number or a numeric string (e.g., "123").
- **is_null()**	Checks if the variable has the value NULL.

# Example

```Php
<?php
$data = "PHP is fun";
$count = 123;
$boolean = true;

// 1. is_int()
if (is_int($count)) {
    echo "Count is a whole number.<br>"; // This executes
}

// 2. is_string()
if (is_string($data)) {
    echo "Data is text.<br>"; // This executes
}

// 3. is_bool()
if (is_bool($boolean)) {
    echo "Boolean is true or false.<br>"; // This executes
}
?>
```