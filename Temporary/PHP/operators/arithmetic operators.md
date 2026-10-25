php offers the same arithmetic operators as other languages such as python. That is why i wont explain them in details but instead  i will just list them and write an example for them

- **`+`**	Addition (Calculates the sum of two values)
- **`-`**	Subtraction (Calculates the difference between two values)
* **`*`** Multiplication (Calculates the product of two values)
-  **`/`**	Division (Calculates the quotient of two values)
- **`%`**	Modulus (Calculates the remainder of a division)
* **`**`** Exponentiation (Raises one value to the power of another)

# Example

```Php
<?php
// Define two variables for the operations
$a = 15;
$b = 4;

$addition = $a + $b;

$subtraction = $a - $b;

$multiplication = $a * $b;

$division = $a / $b;

$modulus = $a % $b;

$exponentiation = $a ** 2; // 15 raised to the power of 2 (15 * 15)

echo "Addition (15 + 4): " . $addition . "<br>";
echo "Subtraction (15 - 4): " . $subtraction . "<br>";
echo "Multiplication (15 * 4): " . $multiplication . "<br>";
echo "Division (15 / 4): " . $division . "<br>";
echo "Modulus (15 % 4): " . $modulus . "<br>";
echo "Exponentiation (15 ** 2): " . $exponentiation . "<br>";
?>
```

