is used to connect array elements together and returns a string where all the elements are joined by a specified separator.

# Syntax

```Php
$stringResult = join($separatorString,$array);
```

- **`$separatorString` (OPTIONAL)** : a string that is used to separate the elements of the array when they are joined together. If omitted, the elements are joined without any separator aka an empty string
- **`$array`** : the input array whose elements are to be joined together into a string. if the elements of the array are not string  the will be converted in the same way as [[concatenation]]

# Example

```Php
<?php
$fruits = ["apple", "banana", "cherry"];
$list = join(", ", $fruits); // Joins array elements with ", "
echo $list; // Outputs: apple, banana, cherry
?>
```

