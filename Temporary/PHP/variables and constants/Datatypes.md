php contains alot of datatypes that  are very similar to other programming languages that is why we wont talk much about them

# bool

```Php
<?php
$foo = True; // assign the value TRUE to $foo
?>
```

# Integers

```Php
<?php
$a = 1234; // decimal number
$a = 0123; // octal number (equivalent to 83 decimal)
$a = 0o123; // octal number (as of PHP 8.1.0)
$a = 0x1A; // hexadecimal number (equivalent to 26 decimal)
$a = 0b11111111; // binary number (equivalent to 255 decimal)
$a = 1_234_567; // decimal number (as of PHP 7.4.0)
?>
```

# Float

```Php
<?php
$b = 1.23;
?>
```

# String

can be defined use single quotes `'` or double quotes `"`

```Php
<?php
$a = "Hello World!\n";
echo $a;
$b = 'hello world';
echo $b;
?>
```

## Numerical strings

if a string contains only number then it can be used as numerical

```Php
<?php
$number = 10;
$numericalString = "10";

echo $number + $numericalString; // Outputs: 20
?>
```

# Type casting

just like C you can type cast by writing the datatype inside of parentheses:

- `(int)` - cast to int
- `(bool)` - cast to bool *(default values like 0, 0.0 or "" will be converted to false*
- `(float)` - cast to float
- `(string)` - cast to string
- `(array)` - cast to array
- `(object)` - cast to object

## Example

```Php
<?php
$number_string = "123.45";

// Cast the string to an integer
$integer_value = (int) $number_string;

// Cast the string to a float
$float_value = (float) $number_string;

// Cast the string to a boolean
$boolean_value = (bool) $number_string;


echo "Original type: " . gettype($number_string) . " (Value: " . $number_string . ")<br>";

echo "Casted to (int): " . gettype($integer_value) . " (Value: " . $integer_value . ")<br>";

echo "Casted to (float): " . gettype($float_value) . " (Value: " . $float_value . ")<br>";

echo "Casted to (bool): " . gettype($boolean_value) . " (Value: " . ($boolean_value ? 'true' : 'false') . ")<br>";
?>
```

