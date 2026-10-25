we wont talk about it in details since its the exact same thing in C.

- if also supports fall through when we obey the word `break`
- it also supports `default` if no option is matched

# Example

```Php
<?php
switch ($i) {
    case 0:
    case 1:
    case 2:
        echo "i is less than 3 but not negative";
        break;
    case 3:
        echo "i is 3";
}
?>
```


