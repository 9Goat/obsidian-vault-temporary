they operate the same compared to other programming languages

# Example

```Php
<?php
for ($i = 0; $i < 5; $i++) {
    if ($i === 2) {
        continue; // Skip the rest of the code when $i is 2
    }
    if ($i === 4) {
        break;    // Stop the entire loop when $i is 4
    }
    echo "Current number: $i\n";
}
// Output: 
// Current number: 0
// Current number: 1
// Current number: 3 
?>
```