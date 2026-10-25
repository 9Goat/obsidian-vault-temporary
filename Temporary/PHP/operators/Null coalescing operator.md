is used to check if a variable is set or not by using a syntax very similar to ternary operator

# Syntax 

```Php
$variable = $variable ?? "some default value".

//same as this ternary operator

$variable = isset($variable) ? $variable : "some default value";
```

what it does is check the variable before the `??` operator is set (was defined and not NULL):

- if it is set it will return the value of the variable
- otherwise it will return the default value after `??`

# Example

```Php
<?php
// Traditional way (longer):
$user1 = isset($username) ? $username : 'Guest';

// Null Coalescing Operator way (shorter):
$user2 = $username ?? 'Guest'; 

echo $user2; // Output: Guest

// --- Example where the variable IS set ---
$title = "Mr.";

$greeting = $title ?? 'Unknown';

echo "\n" . $greeting; // Output: Mr.

?>
```
