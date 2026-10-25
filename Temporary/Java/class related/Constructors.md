the constructor is used to initialize objects when they are created. It has the same name as the class and does not have a return type, not even void.

# Syntax

```Java
class className{

className(parameters){
//constructor body
}

}

class differentClass{
//we create an object using the constructor
className objectName = new className(arguments);

}
```

# How it works

- while we could call  the object and initialize its instance variable one by one but that takes more time and is less efficient. and may provides risks such as:
	- forgetting to change an instance variable
	- trying to change an instance variable that cannot be changed *constant*
- with constructors we can just create an object pass the arguments  it asks for to intialize its variable  and not have to worry  about those potential risks
- when an [[Methods & Objects#Objects|objects]] is created using the `new` keyword, Java automatically calls the constructor of the class, which will execute all of its statements.

# Types of contructors

there are 2 types of constructors in java

## Default constructors

when we provide no user defined constructors java will automatically create a constructor for each class that takes **no arguments** which is essentially the same as [[Methods & Objects#Objects|objects]]

### Example

```Java
class Dog {
    String name; // Default value: null
    int age;     // Default value: 0
    public static void main(String[] args) {
        Dog myDog = new Dog(); // Calls the automatic default constructor
        System.out.println("Dog's name: " + myDog.name); // Output: null
        System.out.println("Dog's age: " + myDog.age);   // Output: 0
    }
}
```

## User defined constructors

we can create our own constructors by defining them in the class with the same name as class,inside the constructor we can execute any block of code that we want, typically used for initializing the instance variables. Also we can define the parameters needed for our constructor just like a method which usually is unintialzied variables that are declared inside the class

### Example

```Java
public class Cat {
    String breed;

    // User-defined constructor
    public Cat(String catBreed) {
        this.breed = catBreed;
        System.out.println("Meow iam a cat");
    }

    public static void main(String[] args) {
        Cat myCat = new Cat("Siamese"); // Calls the user-defined constructor
        System.out.println("My cat's breed is: " + myCat.breed);
    }
}
```

# Notes

-  when creating a [[Constructors#User defined constructors|user defined contructor]] it **MUST** have the same name as the class name
-  [[Constructors#User defined constructors|user defined contructors]] can have any number of parameters even  **zero**
- just like [[Methods & Objects#Methods|methods]] constructors can only be created inside a class **AND** we can have multiple constructors inside the same class as long they have different parameters [[Method overloading]]

## Example 1(overloeaded constructors)

```Java
// OverloadedConstructors.java
public class Box {
    double width;
    double height;
    double depth;

    // Constructor 1: No arguments (default box)
    public Box() {
        this.width = 10;
        this.height = 10;
        this.depth = 10;
        System.out.println("Default Box created.");
    }

    // Constructor 2: Three arguments (custom dimensions)
    public Box(double w, double h, double d) {
        this.width = w;
        this.height = h;
        this.depth = d;
        System.out.println("Custom Box created.");
    }

    void displayDimensions() {
        System.out.println("Dimensions: " + width + " x " + height + " x " + depth);
    }

    public static void main(String[] args) {
        Box box1 = new Box(); // Calls Constructor 1
        box1.displayDimensions();

        Box box2 = new Box(5, 3, 2); // Calls Constructor 2
        box2.displayDimensions();
    }
}
```

