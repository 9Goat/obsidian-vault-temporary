we are grouping both functions since they both serve the same purpose which is uppercasing or lowercasing the first character of a string.

# Syntax

```Php
//lower case the first character of a string
$stringResult = lcfirst ($string); 

//upper case the first character of a string
$stringResult = ucfirst($string);

//uppercase the first character of EACH word in a string
$stringResult = ucwords($string,$separator);
```

- if the first character does not have a distinct upper or lower case variant, the original character remains unchanged.
- if the string is empty the result will be empty too
- the **` $separator` (OPTIONAL)** works the same as [[explode()]]

# Example

```Php
<?php
$text = "hello world, how are you?";

// lcfirst(): Lowercases the first character of the string
$lcfirst_result = lcfirst($text);
echo "lcfirst(): " . $lcfirst_result . "\n"; // Outputs: hello world, how are you?

// ucfirst(): Uppercases the first character of the string
$ucfirst_result = ucfirst($text);
echo "ucfirst(): " . $ucfirst_result . "\n"; // Outputs: Hello world, how are you?

// ucwords(): Uppercases the first character of each word
$ucwords_result = ucwords($text);
echo "ucwords(): " . $ucwords_result . "\n"; // Outputs: Hello World, How Are You?

// ucwords() with a custom separator
$text_with_separator = "apple-banana-cherry";
$ucwords_separator_result = ucwords($text_with_separator, '-');
echo "ucwords() with separator: " . $ucwords_separator_result . "\n"; // Outputs: Apple-Banana-Cherry
?>
```

