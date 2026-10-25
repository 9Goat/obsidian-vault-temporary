in this note we will focus mostly on the equality operators since they are a bit different than the usual programming languages

# 1. Equality and Identity Operators


| Operator   | Name              | Checks For                            | Example       | Returns `true` if...                                                  |
| ---------- | ----------------- | ------------------------------------- | ------------- | --------------------------------------------------------------------- |
| **`=*=     | **Equal**         | Value (after type juggling/coercion)  | `10 == "10"`  | The values are numerically or logically equal.                        |
| **`=*=*=** | **Identical**     | Value **AND** Data Type               | `10 === "10"` | The values and data types are equal (This example returns `false`).   |
| **`!=`**   | **Not Equal**     | Different Value (after type juggling) | `10 != "5"`   | The values are not equal.                                             |
| **`<>`**   | **Not Equal**     | Alias for `!=`                        | `10 <> "5"`   | The values are not equal.                                             |
| **`!=*=`   | **Not Identical** | Different Value **OR** Data Type      | `10 !== "10"` | The values or data types are different (This example returns `true`). |

## Example

```Php
<?php
$a = 5;      // Integer
$b = "5";    // String

echo "1. Equal (==): ";
// True: Values are the same after "5" is converted to an integer.
echo ($a == $b) ? 'true' : 'false';

echo "\n2. Identical (===): ";
// False: Values are the same, but types (int vs. string) are different.
echo ($a === $b) ? 'true' : 'false';

echo "\n3. Not Equal (!=): ";
// False: The values ARE equal, even though types differ.
echo ($a != $b) ? 'true' : 'false';

echo "\n4. Not Identical (!==): ";
// True: The types ARE different (int vs. string).
echo ($a !== $b) ? 'true' : 'false';
?>
```

# 2. Magnitude Operators

exactly the same as other languages

| Operator | Name                         | Checks For                  | Example    | Returns `true` if...                                    |
| -------- | ---------------------------- | --------------------------- | ---------- | ------------------------------------------------------- |
| **`>`**  | **Greater Than**             | Strictly greater value      | `10 > 5`   | The left operand is strictly greater than the right.    |
| **`<`**  | **Less Than**                | Strictly lesser value       | `5 < 10`   | The left operand is strictly less than the right.       |
| **`>=`** | **Greater Than or Equal To** | Greater than or equal value | `10 >= 10` | The left operand is greater than or equal to the right. |
| **`<=`** | **Less Than or Equal To**    | Lesser than or equal value  | `5 <= 10`  | The left operand is less than or equal to the right.    |
## Example

```Php
<?php
$a = 5;      // Integer
$b = "5";    // String

echo $a < $b . "<br>";  // Outputs: false (because "5" is converted to 5)
echo $a <= $b . "<br>"; // Outputs: true
echo $a > $b . "<br>";  // Outputs: false
echo $a >= $b . "<br>"; // Outputs: true
?>
```