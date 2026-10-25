just like C operators have an order

| Rank  | Operators                             | Associativity   | Explanation                                 |
| ----- | ------------------------------------- | --------------- | ------------------------------------------- |
| **1** | `**`                                  | Right           | Exponentiation (Highest priority)           |
| **2** | `*`, `/`, `%`                         | Left            | Multiplication, Division, Modulus           |
| **3** | `+`, `-`, `.`                         | Left            | Addition, Subtraction, String Concatenation |
| **4** | `<`, `<=`, `>`, `>=`                  | Non-associative | Relational Comparisons                      |
| **5** | *=*=, !*=*, *=*=*=, !*=*=, `<>`, <*=> | Non-associative | Equality Comparisons                        |
comparisons are non associative since to combine them we use the `&&` and operators / `||` or operator
# Examples

```Php
<?php
// Left-to-right evaluation for equal precedence: (10 / 2) * 5 -> 5 * 5 -> 25
$c = 10 / 2 * 5;
echo " 10 / 2 * 5 = " . $c . "<br>";
?>
```

```Php
<?php
// Left-to-right: ("Result: " . 5) + 5. The string "Result: 5" converts to 0 for addition.
$d = "Result: " . 5 + 5;
echo " \"Result: \" . 5 + 5 = " . $d . " (String converted to 0)<br>"; // Result: 5
?>
```

```Php
<?php
// Arithmetic is higher: (5 + 5) > 9 -> 10 > 9 -> true (1)
$g = 5 + 5 > 9;
echo " 5 + 5 > 9 (True) = " . (int)$g . "<br>";
?>
```

