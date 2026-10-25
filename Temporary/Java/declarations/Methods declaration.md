# Syntax

```java
[access modifiers] {[static] [final]} OR [abstract] returnType methodName([parameterType parameterName, ...]) {
    // method body
}
```

- [[access modifiers]]
- [[Temporary/Java/class related/static]]
- [[final]]
- [[abstract]]
- **returnType**: Specifies the data type of the value that the method returns. If the method does not return any value, its return type is `void`. This can be any [[Datatypes]] or a class type.
- [[how to name identifiers]] for `methodName`.
- **parameters**: A comma-separated list of input values that the method accepts. Each parameter consists of a `parameterType` and a `parameterName`. Methods can have zero or more parameters.

# Example

```java
public class Calculator {

    // A simple method that adds two integers and returns their sum
    public int add(int a, int b) {
        return a + b;
    }

    // A static method that prints a greeting and returns nothing (void)
    public static void greet(String name) {
        System.out.println("Hello, " + name + "!");
    }

    // A final method that calculates the square of a number
    public final double square(double number) {
        return number * number;
    }

    public static void main(String[] args) {
        Calculator myCalc = new Calculator();

        // Calling the 'add' method
        int sum = myCalc.add(5, 3);
        System.out.println("Sum: " + sum); // Output: Sum: 8

        // Calling the static 'greet' method
        Calculator.greet("Alice"); // Output: Hello, Alice!

        // Calling the 'square' method
        double result = myCalc.square(4.5);
        System.out.println("Square: " + result); // Output: Square: 20.25
    }
}
```