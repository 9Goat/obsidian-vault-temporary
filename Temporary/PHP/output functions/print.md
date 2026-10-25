exactly like [[echo]] but it only accepts a single string argument meaning to extend strings we need to use the concatenation operator **.** instead of commas to separate arguments

# Syntax

```Php
print "String that can contain variable inside it"
```

# Example

```Php
<?php
$var = "this is a php variable";
print "Hello World! $var <br>";
print "HelloWorld " . $var . "<br>";
// print "Hello world" , $var; // this will cause an error because of comma
?>
```

