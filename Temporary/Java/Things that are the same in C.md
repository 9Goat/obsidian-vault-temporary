# if statements

```Java
import java.util.Scanner;

public class testingIfStatements{
public static void main (String a[]){

Scanner scanner = new Scanner(System.in);
System.out.print("Enter a number: ");
int number = scanner.nextInt();

if (number > 0) {
System.out.println("The number is positive.");
} else if (number < 0) {
System.out.println("The number is negative.");
} else {
System.out.println("The number is zero.");
}
scanner.close();
}

}
```

# while loops

```Java
public class whileLoops {
public static void main(String args[]){

int i = 0;
while (i < 5) {
System.out.println("Value of i: " + i);
i++;
}

}
}
```

## Do while loops 

```Java
public class whileLoops {
    public static void main(String args[]){
        int i = 0;
        do {
            System.out.println("Value of i: " + i);
            i++;
        }while(i < 5);
    }
}

```
# for loops

```Java
public class forLoops {
public static void main(String[] args) {

for (int i = 0; i < 5; i++) {
System.out.println("Value of i: " + i);
}
}
}
```

# Ternary operators

```Java
public class ternaryOperators {
public static void main(String[] args) {

int a = 5;
int b = 10;
int max = (a > b) ? a : b;

System.out.println("Max value: " + max);

}
}
```

# Switch statements

```Java
public class SwitchStatementExample {
    public static void main(String[] args) {
        int day = 3;
        String dayName;

        switch (day) {
            case 1:
                dayName = "Monday";
                break;
            case 2:
                dayName = "Tuesday";
                break;
            case 3:
                dayName = "Wednesday";
                break;
            default:
                dayName = "Unknown";
                break;
        }
        System.out.println("Day is: " + dayName);
    }
}
```

# Logical operators

```Java
public class LogicalOperatorsExample {

    public static void main(String[] args) {
        boolean isSunny = true;
        boolean isWarm = false;

        // AND (&&)
        System.out.println("Is it sunny AND warm? " + (isSunny && isWarm)); // false

        // OR (||)
        System.out.println("Is it sunny OR warm? " + (isSunny || isWarm));   // true

        // NOT (!)
        System.out.println("Is it NOT sunny? " + (!isSunny));              // false
    }
}
```

# break

```Java
public class WhileBreakExample {

    public static void main(String[] args) {
        int count = 0;
        while (true) { // An infinite loop
            System.out.println("Count: " + count);
            count++;
            if (count == 3) {
                break; // Exits the while loop when count reaches 3
            }
        }
        System.out.println("Loop ended.");
    }
}
```

