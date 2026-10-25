a scope is an area where a particular variable is accessible within the  program

# How does a scope works?

when we declare a variable within a region of our program (*lets say a method for example*) we can access that variable within that region and, depending on the type of scope, possibly in other regions/scopes (nested scopes) too.But we **CANNOT** access that variable **OUTSIDE** the region/scope we created it in

## Example

```Java
public class MethodScopeExample {

    public static void demonstrateScope() {
        String methodVariable = "I'm inside the method."; // Method-scoped variable

        if (true) {
            // 'methodVariable' is accessible within this nested block
            System.out.println("Inside if block: " + methodVariable);
        }

        System.out.println("Inside method: " + methodVariable);
    }

    public static void main(String[] args) {
        demonstrateScope();
        // The following line would cause a compile error:
        // System.out.println(obj.methodVariable); // 'methodVariable' is not accessible here
    }
}
```

# Different types of scope
## Class scope

every thing inside the class even nested scopes will be able to access variables created within that scope

### Example 

```Java
public class ClassScopeExample {
    String message = "Hello from class scope!"; // Class-scoped variable

    public void displayMessage() {
        System.out.println(message); // Accessible within the method
    }

    public static void main(String[] args) {
        ClassScopeExample obj = new ClassScopeExample();
        obj.displayMessage(); // Output: Hello from class scope!
    }
}
```

## Method Scope

Variables declared within a method are only accessible within that method.

### Example

```Java
public class MethodScopeExample {

    public void showMethodScope() {
        String greeting = "Hello from method!"; // This variable is method-scoped
        System.out.println(greeting); // Accessible here
    }

    public static void main(String[] args) {
        MethodScopeExample obj = new MethodScopeExample();
        obj.showMethodScope(); // Output: Hello from method!

        // System.out.println(obj.greeting); // Compile error: 'greeting' is not accessible here
    }
}
```

## Block Scope

Variables declared within a block (such as if, for, while, etc.) are only accessible within that block. A block is defined by a pair of curly brackets `{}`.

### Example

```Java
public class BlockScopeExample {

    public static void main(String[] args) {
        int x = 10; // This is method-scoped

        if (x > 5) {
            String blockMessage = "Inside the block!"; // This variable is block-scoped
            System.out.println(blockMessage); // Accessible here
        }

        // System.out.println(blockMessage); // Compile error: 'blockMessage' is not accessible here
    }
}
```

## Loop scope

Variables declared within the initialization part of a for loop are only accessible within that loop [[Scope#Block Scope|Block scope]]

### Example

```Java
public class LoopScopeExample {

    public static void main(String[] args) {
        for (int i = 0; i < 3; i++) {
            System.out.println("Current i: " + i); // 'i' is accessible here
        }

        // System.out.println(i); // Compile error: 'i' is not accessible here
    }
}
```
