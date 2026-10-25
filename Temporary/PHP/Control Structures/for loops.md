also very similar to for loops in C so i wont explain them (it also supports multiple expressions separated with commas)

# Example

```Php
<?php
// Initialize multiple variables, and increment multiple variables
for ($i = 0, $j = 5; $i < 5; $i++, $j--) {
    echo "i: $i, j: $j\n";
}
?>
```