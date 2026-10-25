enhances switch statements added in java version 13+ have added quality of life changes and improvements to the standard switch statements

# Multiple labels in a single case

unlike the standard switch statement, the enhanced switch statement allows multiple labels separated by commas in a single case.

## Syntax

```Java
switch ( variable){
case value1,value2,value3,,,,valueN:
statements;
break;
}
```

## Example

```Java
public class MultipleLabelsColonSwitchExample {
    public static void main(String[] args) {
        int dayOfWeek = 6; // 1=Monday, 7=Sunday
        String dayType;

        switch (dayOfWeek) {
            case 1, 2, 3, 4, 5:
                dayType = "Weekday";
                break;
            case 6, 7:
                dayType = "Weekend";
                break;
            default:
                dayType = "Invalid day";
                break;
        }
        System.out.println("Day " + dayOfWeek + " is a " + dayType);
    }
}
```

# Scope

when we declare a variable inside a case statement it has the same scope as the switch block, not limited to the case statement. to fix this we have to surround the block of code within the case statement with curly braces **`{}`**

## Syntax

```Java
switch (value){
case value1:
int variable = someValue; //this variable is visible to the entire switch scope
statements;
break;
case value2: {
int variable = someOtherValue; //this variable is only limited to the case block due to the use of curly braces
statements;
break;
}
}
```

## Example

```Java
public class enhancedSwitch {

    public static void main(String[] args) {
        int choice = 1;
        String commonVariable = "Initial Value";

        switch (choice) {
            case 1:
                commonVariable = "Declared in Case 1";
                System.out.println("Case 1: " + commonVariable);

            case 2:
                // 'commonVariable' from case 1 is still in scope here.
                System.out.println("Case 2: " + commonVariable);
                break;

            case 3: { // Curly braces limit 'scopedVariable' to this block
                String scopedVariable = "Declared inside Case 3's block";
                System.out.println("Case 3: " + scopedVariable);
                break;
            }
            // 'scopedVariable' is not accessible here.

            default:
                System.out.println("Default case");
                break;
        }
    }
}
```

# Switch as expression


switch can be used as a mini method in a sense that i can return a value and assign it to variable
by using the  keyword **`yield`**

when using the switch expression, we **MUST** have a return value otherwise our code will be invalid

## Syntax

```Java
datatype result = switch (variable){
//case statements
}
```

## Yield

yield is the equivalent of using **return** in a method in a sense that, it terminates the switch expression and returns the value specified by the yield statement.

### Syntax

```Java
datatype result = switch (variable){
case value1:
yield value2;
//other case statements
}
```

if our variable has the same value as `value1` the **`yield`** keyword will return `value2` and assign it to `result`, effectively exiting the switch expression.

## Example

```Java
public class SwitchYieldExample {

    public static void main(String[] args) {
        int dayOfWeek = 3; // Let's say 1 for Monday, 2 for Tuesday, etc.

        String dayType = switch (dayOfWeek) {
            case 1, 2, 3, 4, 5:
                yield "Weekday";
            case 6, 7:
                yield "Weekend";
            default:
                yield "Invalid Day";
        };

        System.out.println("Day " + dayOfWeek + " is a: " + dayType); // Output: Day 3 is a: Weekday
    }
}
```

# arrow operator

we use the arrow operator ***mostly*** when we are dealing with a single statement code inside a case

## Syntax

```Java
case value1 -> //single statement code
```

## Example

```Java
public class SwitchArrowStatementExample {

    public static void main(String[] args) {
        int dayOfWeek = 3;

        System.out.print("Day " + dayOfWeek + " is a: ");

        switch (dayOfWeek) {
            case 1, 2, 3, 4, 5 -> System.out.println("Weekday");
            case 6, 7 -> System.out.println("Weekend");
            default -> System.out.println("Invalid Day");
        }
        // Output: Day 3 is a: Weekday
    }
}
```

## Notes


- the arrow operator does **NOT** allow a fall through to happen compared to the standard **`:`** operator after a case statement
- the arrow operator can  be used **ONLY** with a single statement trying to execute more than a single statement after using the arrow operator **WITHOUT** the curly brackets will result in a compiler error
	- to fix this we surround out multi statement code with curly brackets **`{}`**

### Example

```Java
public class SwitchArrowMultiStatementExample {

    public static void main(String[] args) {
        int choice = 2;

        switch (choice) {
            case 1 -> System.out.println("Single statement after arrow.");

            case 2 -> {
                System.out.println("Multiple statements after arrow.");
                System.out.println("This is the second statement.");
            }

            default -> System.out.println("Default case.");
        }
    }
}
```

- when dealing with [[enhanced switch statements#Switch as expression|switch as expression]] with [[enhanced switch statements#arrow operator|arrow operator]] there are 2 ways to return a value:
	- using the [[enhanced switch statements#Yield|yield keyword]] surrounded by curly brackets **`{}`** since its considered 2 statements instead of 1
		- **`yield`** is considered the first statement
		- **`returnValue`** is considered the second statement
	- or by simply writing the return value/expression the compiler will recognise that we are using the arrow operator to return that field without having to use [[enhanced switch statements#Yield|yield keyword]] 

### Example

```Java
public class SwitchExpressionArrowReturnExample {

    public static void main(String[] args) {
        int choice = 2;

        String result = switch (choice) {
            case 1 -> "Direct Return"; 
            case 2 -> {
                yield "Return with Yield Keyword";
            }
            default -> "Unknown Choice";
        };

        System.out.println("Result: " + result);
    }
}
```

