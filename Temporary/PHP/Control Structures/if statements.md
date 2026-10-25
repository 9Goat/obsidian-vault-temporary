the reason why im writing this note is because there are differences between if statements in php than other languages.But they are still fairly similar to C if statements

# different syntaxs

```php
if (condition)
//single statement

if (condition){
//statements
}

if (condition):
//statements
endif;
```

# Example

```Php
<?php

$score = 75;

if ($score >= 90) {
    echo "A";
} elseif ($score >= 80) {
    echo "B";
} else {
    echo "C"; // This is the output
}

?>
```

# Notes

- if php the else if statement is written as **elseif**
- we can write [[Temporary/PHP/Control Structures/if statements]] without using curly brackets, but using a colon **:** and **endif;** at the end of our [[Temporary/PHP/Control Structures/if statements]]

## Example 1

```Php
<?php

$score = 75;

if ($score >= 90):
    echo "A";
elseif ($score >= 80):
    echo "B";
else:
    echo "C"; // This is the output
endif; // The required keyword to close the structure

?>
```
