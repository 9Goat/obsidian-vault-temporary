they are just like other programming languages a variable that can hold multiple values. there are 3 ways to write an array in php

# Syntax

```Php
$array = [value1, value2, value3];

$array2 = array(value1, value2, value3);

$array3 = array(keyValue1 => value1, keyValue2 => value2, keyValue3 => value3);
```

# Explanation

- the first 2 methods to create an array are practically the same where you access elements with they index ordered number
- the third method allows you to specify a custom key for each value, which can be a string or an integer, and you can access the elements using these keys.

# foreach with arrays

foreach has 2 usages with are iterating through arrays and objects. here we will mainly focus of the arrays part

## Syntax

```Php
foreach($arrayName as $elementName){
//statements here
}

// if you want instead to display index/key of the elements
foreach($arrayName as $key=>$value){
//statements here
}
```

# Example

```Php
<?php
$array = ["one", "two", "three", "four"];
$array2 = array("apple", "banana", "cherry", "date");
$array3 = array("item1" => "Alpha", "item2" => "Beta", "item3" => "Gamma", "item4" => "Delta");

echo "<h2>1. \$array (Keys: 0, 1, 2, 3)</h2>";
foreach ($array as $value) {
    echo "Value: " . $value . "<br>";
}


echo "<h2>2. \$array2 (Keys: 0, 1, 2, 3)</h2>";
foreach ($array2 as $key => $value) {
    echo "Key: <b>" . $key . "</b>, Value: " . $value . "<br>";
}

echo "<h2>3. \$array3 (Keys: item1, item2, item3, item4)</h2>";
foreach ($array3 as $key => $value) {
    echo "Key: <b>" . $key . "</b>, Value: " . $value . "<br>";
}
?>
```

# Notes

- the third array method is called associative array
- it is possible to mix both indexed and assortative elements in a single array
- if the key of the indexed array is an integer then it will also change the order of the elements after it (this also applies to associative array)

## Example 1

```php
<?php
$fruits = ["apple", "banana"]; // Keys are 0, 1

// Assign an integer key (e.g., 5) to the next element
$fruits[5] = "cherry";

// Add more elements without specifying keys
// PHP will assign the next available integer key, which is 5 + 1 = 6
$fruits[] = "date";
$fruits[] = "elderberry";

echo "<pre>";
print_r($fruits);
echo "</pre>";
?>
```

## Example with associative 2

```Php
<?php  
$array = array(  
"a",  "b",  6 => "c",  "d");  
var_dump($array);  
?>
```

- just like other programming languages we can create multidimensional arrays in php

## Example 3

```Php
<?php

// A 2D array representing a list of students and their grades
$students = [
    ["Alice", 85],
    ["Bob", 92],
    ["Charlie", 78]
];

// To access Bob's grade (it's in the second element [1], and the second item within that element [1])
echo $students[1][1]; // Output: 92

?>
```

