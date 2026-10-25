the random class is used to get a random outcome whether that is an integer or a double or a boolean...etc

# Syntax

**`import java.util.Random;`**

# Using the random

we need to create an object of that random class to access it and  here is how 

**`Random variable = new Random()`**

# Random integers

by using the **.nextInt()**

## Syntax

```Java
Random rand = new Random();
int variable = rand.nextInt(parameters if needed);
```

## Notes

- if we use the **nextInt** without parameters we will get a random number from **-2b** to positive **2b**
- otherwise if we provide a single parameter ***N*** we will get a random number from **0** to ***N-1**
	- **Example**: `rand.nextInt(6);` will give us a random integer from 0 to 6-1 or **5**
	- **Note** : the number ***N*** **MUST** be positive and different to **0** otherwise we will get an error
- otherwise if we provide 2 parameters ***K , N with K<N*** we will get a random integer from **K** to **N-1** because **K** is inclusive with **N** in exclusive
	- **Example**: `rand.nextInt(-5,10);` we get us a result from -5 to 10-1 or **9**

## Example

```Java
import java.util.Random;

public class random {
public static void main(String[] args) {

Random random = new Random();

int randomNumber = random.nextInt(100);

System.out.println("Random integer: " + randomNumber);

}
}
```

# Random doubles

by using the **`nextDouble()`**

## Syntax

```Java
Random rand = new Random();
double variable = rand.nextDouble(); //no paramters
```

## Notes 

- **`nextDouble`** is a method that takes **NO PARAMTERS** and will always give us a random number from **0.0** to **1**
- if we want to set range (**from K to N**) to that double we have to apply this formula
	- **`double result = K + (rand.nextDouble() * (N - K));`**

## Example

```Java
import java.util.Random;
import java.util.Scanner;

public class random {
public static void main(String[] a) {

Scanner scanner = new Scanner(System.in);

System.out.println("enter both double intervals to geneate a random double number between K and N");

System.out.print("Enter the lower bound (K): ");
double lowerBound = scanner.nextDouble();

System.out.print("Enter the upper bound (N): ");

double upperBound = scanner.nextDouble();
Random rand = new Random();

double randomNumber = lowerBound + (upperBound - lowerBound) * rand.nextDouble();

System.out.println("Random Number: " + randomNumber);

scanner.close();

}
}
```

# Random float

same exact thing as [[Random#Random doubles|random doubles]]

## Example
# Random boolean

by using the **`nextBoolean`**

## Syntax

```Java
Random rand = new Random();
boolean variable = rand.nextBoolean(); //no paramters
```

## Notes

- the same thing as [[Random#Notes|random double]] except that instead of getting a random double from **0.0** to **1** we instead get either **true** or **false**

## Example

```Java
import java.util.Random;

public class random {
public static void main(String[] a) {

Random rand = new Random();

boolean boolValue = rand.nextBoolean();

System.out.println("Random Boolean: " + boolValue);

}
}
```

