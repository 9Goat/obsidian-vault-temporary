is used to get and return the datatype of variables as a string,the datatypes available for return can be found at [[is_datatype()]]

# Syntax

```Php
$stringResult = gettype($variable);
```

# Example

```Php
<?php
$a = 10;
$b = 3.14;
$c = 'Hello';
$d = array('x', 'y');
$e = true;

echo gettype($a); // Output: integer
echo "\n";
echo gettype($b); // Output: double
echo "\n";
echo gettype($c); // Output: string
echo "\n";
echo gettype($d); // Output: array
echo "\n";
echo gettype($e); // Output: boolean
?>
```