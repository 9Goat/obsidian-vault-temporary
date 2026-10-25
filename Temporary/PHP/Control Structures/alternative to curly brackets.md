php offers a way to use control structures without he need for curly brackets by instead starting it with colons **:** and ending it with a specific ending statement, such as "endfor", "endif", or "endwhile" for example

# Syntax

```Php
controlStructure(parameter) :
// statements  to execute
endControlStructure;
```

this applies to the following control structures:

- **`if`**: Ends with **`endif;`**
- **`for`**: Ends with **`endfor;`**
- **`while`**: Ends with **`endwhile;`**
- **`foreach`**: Ends with **`endforeach;`**
- **`switch`**: Ends with **`endswitch;`**

# Example

```Php
<?php
$a = 10;
for ($i = 0; $i < $a; $i++) :
    echo "The number is: $i <br>";
endfor;
?>
```