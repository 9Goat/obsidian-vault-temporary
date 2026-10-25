not particularity a predefined function but you can extend text using the concatenation operator which is a point **.**

# Syntax

```Php
$resultVariable = $varaible1 . $variable2;

//or we could use the .= operator

$variable1 .= $variable2;
```

concatenation will only return string values meaning it will convert other variables into string

- **Integer (`int`)** → Its numeric string value (e.g., `42` becomes `"42"`).
- **Float (`float` or `double`)** → Its numeric string value (e.g., `3.14` becomes `"3.14"`).
- **Boolean (`true`)** → The string `"1"`.
- **Boolean (`false`)** → An **empty string** (`""`).
- **`NULL`** → An **empty string** (`""`).
- **Array (`array`)** → The string `"Array"`.

# Example

```Php
<?php
$a = "Total: ";    // String
$b = 42;           // Integer
$c = 0.99;         // Float (Double)
$d = true;         // Boolean

$result = $a . $b . " and price is " . $c . " Status: " . $d;

echo $result;
// Output: Total: 42 and price is 0.99 Status: 1
?>
```

