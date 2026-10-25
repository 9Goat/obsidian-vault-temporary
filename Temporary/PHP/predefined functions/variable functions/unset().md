unset is used to either destroy and remove a variable from the memory or to remove a specific element/attribute from arrays/objects

# Syntax

```Php
unset($variable);
```

# Examples

```Php
<?php
$colors = array('red', 'green', 'blue');
print_r($colors);
/*
Output:
Array
(
    [0] => red
    [1] => green
    [2] => blue
)
*/

unset($colors[1]); // Removes 'green'

print_r($colors);
/*
Output:
Array
(
    [0] => red
    [2] => blue
)
*/
?>
```

```Php
<?php
$data = 'Hello World';
echo $data; // Output: Hello World

unset($data);

// echo $data; // This line would cause an "Undefined variable" error/notice
?>
```

