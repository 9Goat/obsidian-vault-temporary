This chapter focuses on creational patterns which are the followings:

- **Abstract Factory:** For creating families of related objects.
- **Singleton:** For ensuring you only ever have one instance of a class.
- **Prototype:** For creating new objects by copying an existing one.

# Introduction

While you usually create an object by simply typing `new MyClass()`, as a program grows, this simple approach can make your code stiff and hard to change. The purpose of creational patterns is to **hide the messy details of how objects are made** so that the rest of your program (the "client") doesn't have to worry about it.


# Abstract factory

we use this pattern to:

- **Provide a single interface** for creating objects that belong together (a family).
- **Isolate the family choice:** It keeps the decision of "which family to use" separate from the rest of the application.
- **Make creation transparent:** The client doesn't need to worry about how the objects are instantiated; it just works with the high-level interfaces.

## Interfaces

there are 2 interfaces in our design pattern which are the followings:

- the factory interfaces that defines the methods that all the factories will use to create their objects
- the products that will be created with the factories, they define the methods for the products

**Factory interface**

our application will be about creating buttons and checkboxes in either windows or mac style

```java
interface AbstractFactory{
    public Button createButton();
    public Checkbox createCheckbox();
}
```

**Products interfaces**

```java
interface Button { 
    void paint(); 
}

interface Checkbox { 
    void paint(); 
}
```

## implementations

there are 2 types of implementations which are the followings:

- the implementation of a product, just like our example a windows style button
- the implementation of a factory that only produces a type/family of products

**Products implementations**

```java
class WindowsButton implements Button {
     public void paint() { 
        System.out.println("Rendering Windows Button"); 
    } 
}

class MacButton implements Button { 
    public void paint() { 
        System.out.println("Rendering Mac Button"); 
    } 
}

class WindowsCheckbox implements Checkbox { 
    public void paint() { 
        System.out.println("Rendering Windows Checkbox"); 
    } 
}

class MacCheckbox implements Checkbox { 
    public void paint() { 
        System.out.println("Rendering Mac Checkbox"); 
    } 
}
```

- since we have a checkbox and buttons for 2 styles, that means we will have to implement 4 classes

**Factories implementation**

```java
class WindowsFactory implements AbstractFactory {
    public Button createButton() {
        return new WindowsButton();
    }
    public Checkbox createCheckbox() {
        return new WindowsCheckbox();
    }
}

class MacFactory implements AbstractFactory {
    public Button createButton() {
        return new MacButton();
    }
    public Checkbox createCheckbox() {
        return new MacCheckbox();
    }
}
```

- factories implementations are used to create a new object and immediately return it to the user/client that is using the factory
- it returns the interface button and not the specific button, which is useful for the client since it doesnt have to worry about which button it is interacting with

## Client

finally we have the client/application that will create the product with the factory and execute its methods

```java
class Application {
    private Button button;
    private Checkbox checkbox;

    public Application(AbstractFactory factory) {
        this.button = factory.createButton();
        this.checkbox = factory.createCheckbox();
    }

    public void render() {
        button.paint();
        checkbox.paint();
    }
}
```

- the thing about the client/application is that it does **NOT** know that it produces, it only interacts with the interfaces not the classes directly

![[image-351.png]]
![[image-352.png]]

# Singleton

The **Singleton** pattern is a "creation" pattern with a very specific job: it **guarantees that only one instance** of a class is ever created during the entire time your application is running.

the Singleton pattern has two main goals:

1. **Restrict Instantiation:** It prevents other classes from creating their own versions of this object.
2. **Provide Global Access:** It provides a unique, single method that anyone in the program can use to get that one instance.

## Singleton class

this pattern is by far the easiest since we only will focus on the singleton class itself

```java
class DatabaseConnection {
    private String connectionUrl;
    private static DatabaseConnection instance;

    private DatabaseConnection() {
        this.connectionUrl = "jdbc:postgresql://localhost:5432/production_db";
        System.out.println("DB connection pool to: " + connectionUrl);
    }

    public static DatabaseConnection getInstance() {
        if (instance == null) {
            instance = new DatabaseConnection();
        }
        return instance;
    }

    public void executeQuery(String sql) {
        System.out.println("Executing query [" + sql + "] on connection: " + this.connectionUrl);
    }
}
```

- here is an example of a database connection class, normally when working with a database we should only connect to it once
- we create a new variable called instance that will contain the global database connection that the entire app is going to use
- to make sure that the class cannot be intialized with the new keyword, we make its constructor private
- and we make a new static method that will be used to initialize the object
	- with that method we have to check if the class was intialized with the `null` condition
	- if not we initialize it and return it
	- otherwise we return the already existing global object

## Accessing the singleton class

to access the singleton class we have to use the static method

```java
class ProductService {
    public void viewProduct(int productId) {
        DatabaseConnection db = DatabaseConnection.getInstance();
        db.executeQuery("SELECT * FROM products WHERE id = " + productId);
    }
}

class InventoryService {
    public void checkStock(int productId) {
        DatabaseConnection db = DatabaseConnection.getInstance();
        db.executeQuery("SELECT stock_count FROM inventory WHERE product_id = " + productId);
    }
}
```

- here are have to service that rely on the database connection, for those we have to use the static method to use the private methods of that class

## Multi-threading

the problem with accessing only a single object throughout the project is that, if we for example try to execute the same method of a singleton with multiple threads at the same time we might get a syncronization error where the values dont match or we get a conflict

also an another problem is that if we dont make our getInstance method synchronised we might into a problem of multiple threads creating multiple objects of the singleton

**Solution**

for every method inside the singleton class (except for the constructor) we add the keyword **syncronized** to it

- the only downside of this is a decrease in performance since multiple threads cant execute the same method at the same time and they have to wait in an order

```java
class DatabaseConnection {
    private String connectionUrl;
    private static DatabaseConnection instance;

    private DatabaseConnection() {
        this.connectionUrl = "jdbc:postgresql://localhost:5432/production_db";
        System.out.println("DB connection pool to: " + connectionUrl);
    }

    public static synchronized DatabaseConnection getInstance() {
        if (instance == null) {
            instance = new DatabaseConnection();
        }
        return instance;
    }

    public synchronized void executeQuery(String sql) {
        System.out.println("Executing query [" + sql + "] on connection: " + this.connectionUrl);
    }
}
```

![[image-353.png]]

# Prototype design pattern

the main goals of this pattern are:

- **Copying over Instantiating:** Creating new objects by copying an existing example rather than producing a brand-new, uninitialized instance.
- **Independence:** Allowing a system to create new objects even if it doesn't know exactly which class they belong to.
- **Isolation:** Just like the Abstract Factory, it helps isolate the code from the specific classes being used.

**Why use it?**

- **Performance:** In many cases, **duplicating an existing object is much faster** than creating a new one from scratch using the `new` keyword.

## interface

there 2 ways to use the prototype design pattern:

- create a prototype interface that contains the clone method to override
- use the built in cloneable interface provided by java

```java
interface Prototype {
    public Prototype clone();
}
```

## create the classes that will implement them

in our examples we will be using an abstract class called **shape** and subclasses of rectangle and circle, this part differs depending on the classes we are working with 

```java
abstract class Shape implements Prototype {
    public int x;
    public int y;
    public String color;

    public Shape(int x, int y, String color) {
        this.x = x;
        this.y = y;
        this.color = color;
    }

    @Override
    public abstract Prototype clone();
}


class Circle extends Shape {
    public int radius;

    public Circle(int x, int y, String color, int radius) {
        super(x, y, color);
        this.radius = radius;
    }

    @Override
    public Prototype clone() {
        return new Circle(this.x, this.y, this.color, this.radius);
    }
}


class Rectangle extends Shape {
    public int width;
    public int height;

    public Rectangle(int x, int y, String color, int width, int height) {
        super(x, y, color);
        this.width = width;
        this.height = height;
    }

    @Override
    public Prototype clone() {
        return new Rectangle(this.x, this.y, this.color, this.width, this.height);
    }
}
```

## Client/user

finally we will be showcasing how the client/user can create copies of an already existing objects using the prototype pattern 

```java
public class WithProptotype {
    public static void main(String[] args) {
        System.out.println("Using Prototype Pattern:");
        Circle greenCircle = new Circle(10, 20, "Green", 15);

        Circle clonedCircle = (Circle) greenCircle.clone();

        System.out.println("Original: " + greenCircle.color + " radius " + greenCircle.radius);
        System.out.println("Cloned: " + clonedCircle.color + " radius " + clonedCircle.radius);
    }
}
```

- when cloning its best to typecast the clone into the intended type

## with the cloneable interface

its very similar to the traditional implementation of the prototype pattern but with few changes

```java
public class WithClonablePrototype {
    public static void main(String[] args) throws CloneNotSupportedException {
        System.out.println("Using Prototype Pattern:");
        Circle2 greenCircle = new Circle2(10, 20, "Green", 15);
        
        Circle2 clonedCircle = (Circle2) greenCircle.clone();

        System.out.println("Original: " + greenCircle.color + " radius " + greenCircle.radius);
        System.out.println("Cloned: " + clonedCircle.color + " radius " + clonedCircle.radius);
    }
}


abstract class Shape2 implements Cloneable {
    public int x;
    public int y;
    public String color;

    public Shape2(int x, int y, String color) {
        this.x = x;
        this.y = y;
        this.color = color;
    }

    @Override
    protected Shape2 clone() throws CloneNotSupportedException {
        return (Shape2) super.clone();
    }
}


class Circle2 extends Shape2 {
    public int radius;

    public Circle2(int x, int y, String color, int radius) {
        super(x, y, color);
        this.radius = radius;
    }

}


class Rectangle2 extends Shape2 {
    public int width;
    public int height;

    public Rectangle2(int x, int y, String color, int width, int height) {
        super(x, y, color);
        this.width = width;
        this.height = height;
    }

}
```

- differences:
	- we implement the cloneable interface instead of creating our own
	- we override the clone method in **ONLY** the abstract class by using the clone method of the super class
- inside the clone override method and the main method we have to respect the **CloneNotSupportedException** exception

![[image-354.png]]![[image-358.png]]

