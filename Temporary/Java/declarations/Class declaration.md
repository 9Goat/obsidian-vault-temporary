# Syntax

```java
[access modifiers] [final] OR [abstract] class ClassName {
    // class body:
    // variables, methods, constructors, etc.
}
```

- [[access modifiers]]
- [[final]] (Optional): If `final` is used, the class cannot be subclassed (inherited from).
- `class`: The keyword used to declare a class.
- [[how to name identifiers]] for `ClassName`. By convention, class names start with an uppercase letter and use PascalCase.
- **class body**: Enclosed in curly braces `{}`, this is where you define the members of the class, such as , [[Methods & Objects]], and constructors.

# Example

```java
// A simple class declaration
public class Dog {
    // Instance variable (private for encapsulation)
    private String name;
    private int age;

    // Constructor to initialize a Dog object
    public Dog(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // Getter method for name
    public String getName() {
        return name;
    }

    // Method to make the dog bark
    public void bark() {
        System.out.println(name + " says Woof!");
    }

    public static void main(String[] args) {
        // Creating an instance (object) of the Dog class
        Dog myDog = new Dog("Buddy", 3);

        // Accessing properties and calling methods of the Dog object
        System.out.println("My dog's name is " + myDog.getName()); // Output: My dog's name is Buddy
        myDog.bark(); // Output: Buddy says Woof!

        Dog anotherDog = new Dog("Lucy", 5);
        System.out.println("Another dog's name is " + anotherDog.getName()); // Output: Another dog's name is Lucy
        anotherDog.bark(); // Output: Lucy says Woof!
    }
}

// Example of a final class (cannot be extended)
final class ImmutablePoint {
    private final int x;
    private final int y;

    public ImmutablePoint(int x, int y) {
        this.x = x;
        this.y = y;
    }

    public int getX() { return x; }
    public int getY() { return y; }
}

// class ExtendedPoint extends ImmutablePoint { } // This would cause a compile-time error
```