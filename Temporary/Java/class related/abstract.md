abstract is used to disable the implementation of a class or method, this is useful when we have a parent class that we dont want to create an object but instead we want to create object of its child classes.

# Syntax

```Java
abstract class className{
   //class body
   abstract returnType methodName(parameters);
   //an abstract method CANNOT have a method body meaning no curly brackets{}
}
```

# How it works

abstract is useful when we have a generic parent class that we dont want to create an object of lets say *animal* for example ,creating a object of *animal* wouldn't make much sense because it's too general, instead we want to create objects of its child classes like *dog*, *cat*, or *bird*. To prevent the user from  creating an object of *animal* we make it an abstract class (which prevents it from creating an object),

This also applies to abstract methods lets say we have an abstract class called *shape* and we want to measure the area of different shapes. We can declare an abstract method called `calculateArea()` in the `Shape` class, which will be implemented differently by its child classes like `Circle`, `Rectangle`, or `Triangle`.  since the method is abstract that means it **CANNOT** be called from the parent class

we use abstract to decide which methods we want our child classes to have its the equivalent of blue print

# Example

```java
abstract class Vehicle {
    abstract void drive(); // Abstract method: no body
}

class Car extends Vehicle {
    @Override
    void drive() {
        System.out.println("Car is driving.");
    }
}

public class AbstractExample {
    public static void main(String[] args) {
        // Vehicle myVehicle = new Vehicle(); // ERROR: Cannot instantiate abstract class
        Car myCar = new Car();
        myCar.drive();
    }
}
```

# Notes

- you can have as many abstract classes as we want
- it is not possible to create an instance of an abstract class, or class of one its abstract methods
	- BUT we can create a variable with the datatype of that abstract class as long as we dont turn it into an object instance
		- **Example**: this is correct: `Animal animal;`
- an abstract method can **ONLY** be created inside an abstract class
- in an abstract class we can have both standard methods and abstract methods
- an abstract method **CANNOT** have a body meaning instead of using curly brackets for abstract methods we instead close it with semi colones `;`
- an abstract class can be created without a child class this will **NOT** cause a compile error since java will just ignore its existence 
- when we extend an abstract class, we are **REQUIRED** to [[method overriding|override]] them otherwise we will get a compile error 