final is a keyword used to declare constants meaning they:

- **MUST** be intialized otherwise we will end up with *blank variable* that holds the default value and cannot be changed
- and they cannot change their initial value

# constant variables

## Example

```Java
public class FinalVariableDemo {
    public static void main(String[] args) {
        final int MAX_VALUE = 100; // Declared and initialized as final

        System.out.println("Max Value: " + MAX_VALUE); // Output: Max Value: 100

        // MAX_VALUE = 200; // This line would cause a compile-time error:
                          // "cannot assign a value to final variable MAX_VALUE"
    }
}
```

# Constant methods

final methods mean that the method **CANNOT** be [[method overriding|overriden]]

## Example

```Java
public class Parent {
    
    // This method's behavior MUST NOT be changed by any subclass.
    public final void criticalCalculation() {
        System.out.println("Executing the guaranteed, final algorithm.");
    }

    // A normal method that can be overridden.
    public void standardAction() {
        System.out.println("Performing a standard action.");
    }
}

public class Child extends Parent {
    
    // ERROR: Compile-time error! Cannot override a final method.
    // public void criticalCalculation() {
    //     System.out.println("Trying to change the algorithm."); 
    // }

    // This is fine, as standardAction is not final.
    @Override
    public void standardAction() {
        System.out.println("Child is performing a modified standard action.");
    }
}
```

# Constant classes

When a class is declared with the final keyword in Java, it is called a final class. A final class cannot be extended([[Temporary/Java/class related/inheritance]]).

## Example

```Java
final class A
{
     // methods and fields
}
// The following class is illegal
class B extends A 
{ 
    // COMPILE-ERROR! Can't subclass A
}
```

