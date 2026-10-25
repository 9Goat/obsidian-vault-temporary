ord is the opposite of [[chr()]] it take a string and returns an integer representing the code ASCII of **FIRST** character

# Syntax

```Php
$intResult = ord($stringVariable);
```

# Example

```Php
<?php
$text = "Hello";
$code = ord($text);
echo $code; // Output: 72 (The ASCII code for 'H')
?>
```

