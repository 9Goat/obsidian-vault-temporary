echo is used to display messages which can contain  strings and variables inside them.Echo  can task as many arguments as possible separated by commas

# Syntax

```Php
echo "string and variables in here"
echo "string" ,variable,,,,;
echo "string" .varible...;
```

- in php you can write variables inside of strings
- if you want to perform certain actions with strings like adding you can separte the strings from the variable and add them together by using either **.** point(*which is called string concentration*) or **,** comma

# Example

```Php
<?php
$var = "this is a php variable";
echo "Hello World! $var <br>";
echo "HelloWorld " , $var , "<br>";
echo "HelloWorld " . $var . "<br>";
?>
```

