both functions are extremely simliar to [[String methods#startsWith()|startsWith()]] and [[String methods#endsWith()|endsWith()]] so i wont explain them in details except that it is case sensitive *it treats lower case and upper case as DIFFERENT*

# Syntax

```Php
//starts With

$booleanResult = str_starts_with($stringVariable, $searchString);

//ends with

$ booleanResult = str_ends_with($stringVariable, $searchString);
```

# Example

```Php
<?php
$text = "Hello World";

// str_starts_with()
echo str_starts_with($text, "Hello") ? "Starts with 'Hello'\n" : "Does not start with 'Hello'\n"; // Outputs: Starts with 'Hello'

// str_ends_with()
echo str_ends_with($text, "world") ? "Ends with 'World'\n" : "Does not end with 'World'\n";   // Outputs:Does not ends with 'World' //case sensitive
?>
```
