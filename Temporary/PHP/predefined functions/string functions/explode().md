is used to return an array of strings by choosing the separator and the limit. The separator is used to determine where to split the string, and the limit is used to specify the maximum number of elements to be returned in the resulting array.

# Syntax

```Php
$arrayResult = explode($separator, $string, $limit); 
```

- **`$separator` (REQUIRED)**: The separator is the string that determines where each split occurs in the original string.
- **`$string` (REQUIRED)**: The input string to be split into an array.
- **`$limit` (OPTIONAL):** The limit parameter is used to determine the length of the resulting array
	- If `$limit` is **positive**, the resulting array will have at most that many elements. The last element will contain the rest of the string.
	- If `$limit` is **negative**, it excludes the last `$limit` elements from the resulting array.
	- If `$limit` is **0** (or omitted), it defaults to `PHP_INT_MAX`, returning all possible segments.

# Example

```Php
<?php
$csv = "apple,banana,cherry";
$path = "/products/laptops/apple";
$text = "PHP is very powerful, flexible, and popular.";
$long_list = "one--two--three--four--five";

// 1. Basic Split
$fruits = explode(",", $csv);
var_dump($fruits);
// Output: array(3) { [0]=> string(5) "apple" [1]=> string(6) "banana" [2]=> string(6) "cherry" }

// 2. Split with Path Delimiter (Starting with delimiter creates empty string at [0])
$segments = explode("/", $path);
var_dump($segments);
// Output: array(4) { [0]=> string(0) "" [1]=> string(8) "products" [2]=> string(7) "laptops" [3]=> string(5) "apple" }

// 3. Positive Limit (Array stops at 3 elements)
$parts = explode(" ", $text, 3);
var_dump($parts);
// Output: array(3) { [0]=> string(3) "PHP" [1]=> string(2) "is" [2]=> string(32) "very powerful, flexible, and popular." }

// 4. Negative Limit (Excludes the last 2 elements)
$shortened = explode("--", $long_list, -2);
var_dump($shortened);
// Output: array(3) { [0]=> string(3) "one" [1]=> string(3) "two" [2]=> string(5) "three" }
?>
```

