the continue keyword is a flow control statement (**for loops, while loops, and do-while loops**) that is used to **SKIP** an iteration and immediately just to the next iteration

skipping an iteration means ignore the rest of the code inside the loop for the current iteration, and then proceed with the next iteration.

# Syntax

```Java
loopStatement {
if (condition){ //a contdition to skip a certain iteraion within our loop
continue ;
}

}
```

# Example

## Example with a for-loop

```Java
public class continueInForLoops {
    public static void main(String[] args) {
        for (int i = 0; i < 5; i++) {
            if (i == 2) {
                continue; // Skip the rest of the loop when i is 2
            }
            System.out.println("Value of i: " + i);
        }
    }
}
```

## Example with a while-loop

```Java
public class WhileContinueExample {

    public static void main(String[] args) {
        int i = 0;
        while (i < 5) {
            i++;
            if (i == 3) { //skipping the iteration when the value is 3
                continue;
            }
            System.out.println("Value: " + i);
        }
    }
}
```