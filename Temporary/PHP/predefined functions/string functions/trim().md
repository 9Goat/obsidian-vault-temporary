trim function is a common function in programming languages that removes leading and trailing whitespace from a given string, but in php there are 2 additional versions of this function, namely ltrim and rtrim, where ltrim removes only the leading whitespace, and rtrim removes only the trailing whitespace. 

# Syntax

```Php
//removes both leading and tailing whitespace from a given string.
$stringResult = trim($stringVariable);

//removes only the leading whitespace from a given string.
$stringResult = ltrim($stringVariable);

//removes only the trailing whitespace from a given string.
$stringResult = rtrim($stringVariable);
```

# Example

```Php
<?php
$string = [
    "   Hello, World!   ",
    "   PHP is fun!   ",
    "   Let's code!   "
];

echo "<pre>"; // Start pre-formatted text

echo "--- trim() (Both Sides) ---<br>";
echo "|", trim($string[0]), "|"; 

echo "<br>--- ltrim() (Left Side Only) ---<br>";
echo "|", ltrim($string[1]), "|"; 

echo "<br>--- rtrim() (Right Side Only) ---<br>";
echo "|", rtrim($string[2]), "|";

echo "</pre>"; // End pre-formatted text
?>
```

- the `<pre>` element in necessary for us to see the result since browsers will automatically convert multiple of whitespaces into just a single