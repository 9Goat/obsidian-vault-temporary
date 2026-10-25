same thing as C since they also support pre increment and post increment operations

# Example

```Php
<?php

// --- Pre-Increment/Decrement ---
$a = 5;
$b = ++$a; // $a is incremented first (to 6), then assigned to $b.
// Output: $a is 6, $b is 6

$c = 10;
$d = --$c; // $c is decremented first (to 9), then assigned to $d.
// Output: $c is 9, $d is 9

// --- Post-Increment/Decrement ---
$x = 5;
$y = $x++; // $x is assigned to $y first (5), then $x is incremented (to 6).
// Output: $x is 6, $y is 5

$z = 10;
$w = $z--; // $z is assigned to $w first (10), then $z is decremented (to 9).

echo "a is $a, b is $b<br>"; // Output: a is 6, b is 6
echo "c is $c, d is $d<br>"; // Output: c is 9, d is 9
echo "x is $x, y is $y<br>"; // Output: x is 6, y is 5
echo "z is $z, w is $w<br>"; // Output: z is 9, w is 10
?>
```

