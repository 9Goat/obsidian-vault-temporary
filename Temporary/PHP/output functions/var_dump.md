is an output method use for debugging.What it does it output the datatype of the variables within the parameters and their values respectively

# Syntax

```Php
var_dump($varaible1,$variable2,,,,$variableN);
```

- for example if we have `$x = 4` var_dump will output:
	- **int(4)**

# Example

```Php
<?php
$var = "this is a php variable";
$var2 = 4;
$var3 = 5.5;
$var4 = true;
$var5 = array("apple", "banana", "cherry");
echo "<pre>";
var_dump($var);
echo "<br>";
var_dump($var2);
echo "<br>";
var_dump($var3);
echo "<br>";
var_dump($var4);
echo "<br>";
var_dump($var5);
echo "</pre>";
?>
```

# Notes

it is good practice to output the result of [[var_dump]] by wrapping it in `<pre>` tags to maintain the formatting of the output, making it more readable.