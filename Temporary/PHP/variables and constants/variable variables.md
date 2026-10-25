in php you can create variables that contain other variables

# Syntax

```Php
$variableName = "VariableName2";
$VariableName2 = "value" //this is a variable variable

// to access it we use the $$

echo $$variableName;
```

# variable variables chain

Yes you chain multiple variables to each other and use multiple **$** to access it

## Example

```Php
<?php

$variable = "variable2";
$variable2 = "variable3";
$variable3 = "variable4";
$variable4 = "Hello, World!";

echo $$$$variable; // Outputs: Hello, World! (each $ adds a level of indirection)

?>
```

# Example

```Php
<?php

$variable = "variable2";
$variable2 = "this is a variable variable";

echo $$variable; // outputs "this is a variable variable"

$example2 = "example3";
$$example2 = "this is example3";

echo "<br>";
echo $example3; // outputs "this is example3"

?>
```