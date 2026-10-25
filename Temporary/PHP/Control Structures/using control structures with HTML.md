instead of using html structures to exectly php statements we can instead use it to execute html code

# Syntax

```Php
<?php controlStructure(condition): ?>
//html elements to be executed if condition is true.
<?php endcontrolStructure ?>
```

# Example

```Php
<?php if ($a == 5): ?>
A is equal to 5
<?php endif; ?>

//Example with while
<?php
$a = 1;
while ($a < 5): ?>
<br>
A is equal to <?php echo $a; ?>
<?php $a++; endwhile; ?>
```

