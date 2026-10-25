very similar to [[empty()]] but instead of checking whether a variable has a default value or not it only checks whether a value exists or if it has a **NULL** value

# Syntax

```Php
reutrnVariable = isset(variable); //returns a boolean
```

# Example

```Php
<?php
$a = 0;      // Set, but considered "empty"
$b = null;   // Set to NULL
// $c is undefined
echo "<pre>";
// isset() checks if it's there
var_dump(isset($a)); // TRUE
var_dump(isset($b)); // FALSE (because it's NULL)
var_dump(isset($c)); // FALSE (because it's undefined)

// empty() checks if it's useless
var_dump(empty($a)); // TRUE (because 0 is empty)
var_dump(empty($b)); // TRUE (because NULL is empty)
var_dump(empty($c)); // TRUE (because it's undefined)
echo "</pre>";
?>
```

