this applies to methods ,attributes and classes,,,etc

# Rules to follow 

- **Start Character:** Must begin with a letter (A-Z or a-z), a dollar sign (`$`), or an underscore (`_`).**_**
- **Valid Characters:** After the first character, identifiers can contain letters, digits (0-9), dollar signs (`$`), or underscores (`_`).
- **No Keywords:** Cannot be a Java reserved keyword (e.g., `public`, `static`, `if`, `for`).
- **Case-Sensitive:** Java is case-sensitive, meaning `myVariable` and `MyVariable` are treated as two different identifiers.
- **No Spaces:** White space is not allowed within a name.

# Example

```Java
public class IdentifierExamples {

    // --- Valid Identifiers ---

    // Starts with a letter, contains only letters
    String myVariable = "Valid";

    // Starts with an underscore, contains only letters
    int _count = 10;

    // Starts with a dollar sign, contains only letters
    double $price = 99.99;

    // Starts with a letter, contains letters and digits
    boolean number123 = true;

    // Starts with a letter, contains letters and an underscore
    String calculate_Total = "Result";

    // Common for class names (starts with a letter, contains only letters)
    // class MyClass { /* ... */ } // This would be a separate class definition

    // Starts with an underscore, contains valid characters ($, _, letters)
    long _$_value = 12345L;


    // --- Invalid Identifiers (would cause compile-time errors if uncommented) ---

    // int public = 5; // Invalid: 'public' is a Java reserved keyword

    // int 1stNumber = 20; // Invalid: Cannot start with a digit

    // String my variable = "Invalid"; // Invalid: Contains a space

    // double item-id = 10.5; // Invalid: Contains a hyphen ('-'), which is not a valid character

    // void voidMethod() { /* ... */ } // Invalid: 'void' is a Java reserved keyword (for a method name)
}
```

