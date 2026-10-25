is used to split the string into a defined chunks where all chunks has a specified size (except for the last chunk which might be smaller)

# Syntax

```Php
$arrayResult = str_split($variableString , $intChunkSize);
```

- **`$varaibleString` (REQUIRED)**: the string that is going to be split. 
- **`$intChunkSize` (OPTIONAL)**: the size of each chunk
	- if we omit it,the default value will be 1 (split the string into an array character)
	- otherwise split the string into an array where each element is a substring of the original string with the specified length. (except for the last element which might be smaller if the string length is not perfectly divisible by the chunk size)

# Example

```Php
<?php
$str = "Hello";
$arr = str_split($str); // Splits into individual characters
print_r($arr);
// Output: Array ( [0] => H [1] => e [2] => l [3] => l [4] => o )

$arr_chunks = str_split($str, 2); // Splits into chunks of 2 characters
print_r($arr_chunks);
// Output: Array ( [0] => He [1] => ll [2] => o )
?>
```
