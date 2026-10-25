in java scanners are used to the user input and store it inside a variable and to do that we need to import a package within our code and here is how to do it


# Syntax

write this line at the top of code

`import java.util.Scanner;`

# Using the scanner

to use the scanner we need to create a scanner object

## Syntax

`Scanner scanner = new Scanner(System.in);`

## Explanation

- **Scanner**: Scanner in the datatype of the object we are creating
- **scanner**: this is just a variable name and can be changed to anything we want
- **new Scanner**: this line creates a new instance of a scanner object
- **(System.in)**: System.in is the standard input system we are going to be using to take the user input

# Different types of inputs

to convert the user input to the datatype we want we need to use the appropriate scanner modifier

when we use a scanner modifier for any type it will ask the user for an input and the way they handle user inputs differentiate with the type of scanner modifier

- **`next()`**: used to read a single word as string text
	- **What it does**: Reads the next single word (token) from the input. A "word" is any sequence of characters separated by whitespace (spaces, tabs, newlines).
	- **Delimiter handling**: It skips leading whitespace and reads until the _next_ whitespace character. It _does not_ consume the trailing whitespace
- **`nextLine()`**: used to read the entire user input and converts it to string text
	-  **What it does**: Reads the entire line of input, including spaces, until it encounters the newline character (`\n`) that is generated when you press Enter.
	- **Delimiter handling**: It _does_ consume the newline character.
- **`nextInt()`**: used to read the first word and converts it to an integer if possible
	- **What it does**: Reads the next sequence of characters that can be parsed as an integer (`int`).
	- **Delimiter handling**: It skips **leading** whitespace and reads digits until it hits a non-digit character or a whitespace delimiter. It _does not_ consume the trailing delimiter (e.g., the `\n` from pressing Enter).

- **`nextByte()`, `nextDouble()` , `nextBoolean()` ,  `nextShort()`, `nextLong()`, `nextFloat()`** use the same technique as **nextInt** to convert to their respective type

## Syntax

`datatype variable = scannerObjectName.modifier()`

- the modifier can be any type of scanner inputs from [[Scanners#Different types of inputs|scanner modifiers]] like `nextLine`, and the word scanner represente
- and the scannerObjectName is the just the variable name we used to name the scanner object instance from [[Scanners#Syntax|using the scanner]]

# Note

since modifiers like nextDouble dont remove whitespaces at the end of the input we need to use the nextLine modifier to consume those whitespaces

## Example

```Java
import java.util.Scanner;

public class ShortScannerExample {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter a price (e.g., 19.99): ");
        double price = scanner.nextDouble();

        // Consume the leftover newline character after nextDouble()
        scanner.nextLine();

        System.out.print("Enter a product name: ");
        String productName = scanner.nextLine();

        System.out.println("Price: " + price);
        System.out.println("Product Name: '" + productName + "'");

        scanner.close();
    }
}
```

# Example

```Java
import java.util.Scanner;

public class ShortScannerExample {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter your first name: ");
        String firstName = scanner.next(); // Reads "John"
        System.out.println("First Name: " + firstName);

        System.out.print("Enter your age: ");
        int age = scanner.nextInt(); // Reads "30", leaves '\n'
        System.out.println("Age: " + age);

        scanner.nextLine(); // Consumes the leftover '\n'

        System.out.print("Enter your favorite city (can have spaces): ");
        String city = scanner.nextLine(); // Reads "New York"
        System.out.println("Favorite City: " + city);

        scanner.close();
    }
}

```



