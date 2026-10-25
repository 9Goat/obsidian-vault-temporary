very similar to contains function in other programming languages where it is used to return true or false depending on whether a certain sub string is present in the given string (**uppercase and lowercase letters do matter**) *case sensitive*

# Syntax

```Php
$booleanResult = str_contains($searcheString,$subStringToFind);
```

- **`searcheString`** : represents the main string where we will be searching if the sub string exists or not. 
- **$subStringToFind** : is the sub string that we are looking for within the main string.

# Example

```Php
<?php
$text = "Hello World";

if (str_contains($text, "World")) {
    echo "The string contains 'World'."; // This will be output
} else {
    echo "The string does not contain 'World'.";
}
?>
```
