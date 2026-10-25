very similar to [[switch statement]] but instead of executing a block of code, it returns a value.

# Syntax

```Php
$returnVariable = match(variable to be matched) {
    value1 => returnValue1,
    value2 => returnValue2, //each case is separated by a comma ,
    value3,value4 => returnValue3or4, //mutliple values can be matched by separating them with commas
    default => defaultReturnValue,
};
```

# How it works

- it takes a value to match against multiple values.
- you can specify multiple values to match against by separating them with commas.
- if a value matches it will return the value after **=>**
- matches are separated by commas between every case
- it no matches were met the default will return it value
# Example

```Php
<?php
$status_code = 200;

$message = match ($status_code) {
    200 => 'OK',              // If $status_code is 200, the expression returns 'OK'
    400, 401 => 'Error: Client side issue', // Multiple values separated by commas
    500 => 'Error: Server side issue',
    default => 'Unknown Status Code',
};

echo $message; // Output: OK
?>
```

# Notes

- compared to the switch statement, it compared the values using double equals *=*= instead of triple equals **===
- match does not support fall through and it doesnt require the keyword **break**