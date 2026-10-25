polymorphison stands for many shapes . In object-oriented programming, polymorphism is the ability of an an object or an array to contain many of its children classes. [[Polymorphism]] works for both [[Temporary/Java/class related/inheritance]] and [[interfaces]]

# Syntax

```Java
class className{
public static void main(String args[]){

parentClass[] tableName = {new childClass1(parameters), new childClass2(parameters), new childClass1(parameters), new childClass3(parameters),,,,};

for (parentClass obj : tableName) { 
 obj. methodName(); // calling a method that is overridden in the child classes

}

}
}
```

- in this syntax we defining a table of the parent objects (since the parent object can contain any of its sub classes)
- the point of this so that we can call a method on each object in the table without knowing its actual class type at compile time.
- an index of that array can access the following methods:
	- **Methods defined in the Parent class:** You can call any public or protected method that exists in the parent class.You cannot access methods that exist **only** in the child class.
	- **Overridden methods:** If the child class has **overridden** a method from the parent class, Java will execute the child's version of that method at runtime (this is the core of polymorphism).

# Example

```Java
//lets say that the parent class is called `Animal` and it has a method called `sound()`. which is shared between itself and all of its children using override
class test{
public static void main(String[] args){

Animal[] animalTable = { new Dog(), new Cat(), new Animal()}; 

for (Animal a: animalTable){
a.sound();
}

}
}
```

# Instanceof function

the child objects inside the parent class arrays **CANNOT**  access their specific functions since they are treated as an instance  of the parent  class, so to access those functions we have to use  the function instance of

## Syntax

```JAVA
if (childOjb instanceof parentClass){
// statements here
}
```

the instance of  is used to return true of false if the object in question is an instance of the specified class.

## Usage of Instanceof

To access the specific methods or properties of a child class, you need to cast the object to its actual class type. Before doing that, it's a good practice to check if the object is an instance of that class using `instanceof`. Here's how you can do it:

```java
if (a instanceof Dog) {
    Dog dog = (Dog) a;
    dog.bark(); // Now you can call methods specific to Dog class
}
```

## Example

```Java
public class Main {
  public static void main(String[] args) {
    Main myObj = new Main();
    System.out.println(myObj instanceof Main); // returns true
  }
}
```

