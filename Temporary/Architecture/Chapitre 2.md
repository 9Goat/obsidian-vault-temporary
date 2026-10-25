
# Single Responsibility Principle (Responsabilité Unique)

**The Concept:** A module, class, or function should have **one, and only one, reason to change.** aka only main functionality/responsibility

- **The Goal:** Increase functionalities.
- **The Problem (Immobility):** If a class does too many things, you cannot reuse one part of it without dragging the whole "mess" along. If you change one responsibility, you risk breaking the other one.

## Solution (refactoring)

refactoring is dividing a class into multiple classes

![[image-272.png]]

![[image-273.png]]

this is better for 3 reasons:

- easier to read and maintain
- easier to change without breaking other component
- easier to test

# Open-Closed Principle (Ouverture / Fermeture)

**The Rule:** A software artifact should be **open for extension**, but **closed for modification**.

- **Closed for Modification:** You should not have to change the source code of a class that is already tested and working.
- **Open for Extension:** You should be able to add new behaviors by adding new code.

## Solution

**The "Anti-Pattern" (The `if/else` trap):** Imagine you have a class that calculates shipping costs.

- **Violating OCP:** You have a function `calculate(type)` with an `if (type == "Standard")` and `else if (type == "Express")`. When you want to add "International" shipping, you have to **open and modify** the existing class to add another `else if`.

![[image-274.png]]


###  Code solution

**Interface**

![[image-308.png]]

**options/methods**

![[image-309.png]]

**Implementation**

![[image-310.png]]

**main method**

![[image-311.png]]
# LSP: Liskov Substitution Principle (Substitution de Liskov)

**The Rule:** if an inheritance  result in a logic error

**The Square/Rectangle Example (from your file):** In math, a Square is a Rectangle. In programming, if you make `Square` inherit from `Rectangle`:

1. A `Rectangle` has a contract: "I can set Width and Height independently."
2. A `Square` breaks that contract: "If you set my Width, I will secretly change my Height too."

## Solution

connect square with rectangle via composition and connect both of them with an interface that contains the common methods

![[image-305.png]]

# ISP: Interface Segregation Principle (Ségrégation des Interfaces)

**The Core Idea:** "No client should be forced to depend on methods it does not use."

- **The Problem:** We often create "Fat Interfaces" (interfaces with too many methods). When a class implements a fat interface, it is forced to provide code for methods it doesn't need, usually resulting in empty methods or "Not Implemented" errors.
- **The Goal:** Split large interfaces into smaller, highly specific ones.

## Solution (refactoring)

![[image-275.png]]

![[image-276.png]]

# DIP: Dependency Inversion Principle (Inversion des Dépendances)

Normally, a "High-Level" class (the one that makes decisions) creates and uses a "Low-Level" class (the one that does the dirty work).

**Example: A Password Reminder System**
- **High-Level:** `PasswordReminder` (Decides _when_ to remind the user).
- **Low-Level:** `MySQLConnection` (Actually talks to the database).

In a bad design, `PasswordReminder` has a line of code like: `db = new MySQLConnection()`.
- **The Issue:** The Reminder is now **stuck** to MySQL. If you want to use a different database, you have to break open the Reminder and change its code. The "Brain" is dependent on the "Tool."

## Solution

In a bad design, the high-level class creates its own tools using the `new` keyword.

**The Problem (Violation):** Imagine a `Logger` (High-level) that directly creates a `Filesystem` object (Low-level).
- If you decide to log to a "Database" instead of a "File," you have to rewrite the `Logger`.
- The `Logger` is **dependent** on the `Filesystem`.


Instead of the high-level class looking at the tool, we create a common interface that defines _what_ needs to be done, but not _how_.
**The Solution:** Create an interface called `ILogStorage`. It has one method: `save(message)`.

Now, you change both classes so they only look at the Interface.

1. **The High-Level Class:** The `Logger` now says: "I will take any object that follows the `ILogStorage` contract. I don't care if it's a file, a database, or a cloud service."
2. **The Low-Level Class:** The `Filesystem` and `Database` classes now "implement" the `ILogStorage` interface

![[image-277.png]]

![[image-278.png]]

![[image-279.png]]

![[image-306.png]]

![[image-307.png]]



# Definitions

## The Law of Demeter

when we call submethods of submethods 

```Java
// This breaks the Law of Demeter
String city = student.getLibraryCard().getFavoriteLibrary().getAddress().getCity();
```

**Solution?**: create a method that returns the exact varaible without having to go through all of the others submethods

##  idiom

- **Manual work:** Writing the logic from scratch because you don't know the language's shortcuts.
- **Idiom:** Using the language's specific "shortcuts" because they are safer, faster, and more readable for other developers.

## Peter Coad's Rules

**Use inheritance only when ALL of the following criteria are met:**

### Special Type" vs. "Role Played"

An `Apple` is a special type of `Fruit`. But a `Student` is a **role** a `Person` plays.

- **Bad (Role):** `class Student extends Person`. (What happens when the student graduates? You can't change their class to `Employee` easily).
- **Good (Special Type):** `class CheckingAccount extends BankAccount`.

### 2. Never becomes another subclass

If your object needs to change its nature at runtime, inheritance will break your code.

- **The Trap:** `class FlyingDuck extends Duck`. If the duck gets injured and can't fly, it can't suddenly stop being a `FlyingDuck` object in Java.
- **The Solution:** Use **Composition** (give the Duck a `FlightBehavior`) so you can swap it out.

### 3. Extend, don't Redefine (Liskov Substitution Principle)

Inheritance should be used to **add** new behavior, not to **cancel** or **break** existing behavior.

- **Bad:** Creating a `class Square extends Rectangle` and then overriding `setHeight()` to also change the width. This "redefines" how a rectangle is supposed to work and confuses other parts of your code.

### 4. Not a Utility Class

Don't use inheritance just because you want to "borrow" some code.

- **Bad:** `class UserRepository extends StringUtils`. Just because you want to use string helper methods doesn't mean a Repository **IS-A** String Utility.
- **Better:** Just use the utility class as a static call or inject it.

## libraries

a collection of classes and methods:

- specific to a programming language
- indepdent of each others
- not  built-in by default

## framework

- **A Collection of Classes:** A framework consists of both **abstract** and **concrete** classes.
- **Interdependence:** These classes are specifically designed to be used **together**.
- **Default Behavior:** It provides a "pre-built" or default behavior so you don't have to start from zero.

white box: inheritance
black box: composition 

## pattern

**A conceptual solution for a recurring problem.**

- Logical components described independently of any specific programming language.
- Patterns are represented by models... and comments!
- Patterns are named so they can be communicated (vocabulary).

## anti patterns

**Anti-patterns are common solutions to ineffective problems and cause more problems than they solve.**

It represents a "lesson learned."


# 4 rules

## reduce accessibility of class members

most classes should be treated as services making their members invisible to other classes

### Solution

- make the attributes of a service class private
- reduce the usage of getters and setters
- make those attributes only usable instead the parent class and make the user manipulate them through methods 

## Encapsulate what varies 

This principle is about preventing a "monolithic" class where you use a bunch of `if/else` statements to handle different behaviors. Instead, you move the changing parts into their own classes.

### bad implementation

```Java
public class Duck {
    String type;

    public void performQuack() {
        if (type.equals("Mallard")) {
            System.out.println("Quack!");
        } else if (type.equals("Rubber")) {
            System.out.println("Squeak!");
        } else if (type.equals("Decoy")) {
            System.out.println("<< Silence >>");
        }
    }
}
```

### Solution

```Java
// 1. The Interface (The "Contract" for the behavior)
public interface QuackBehavior {
    void quack();
}

// 2. The Encapsulated Variations
public class Quack implements QuackBehavior {
    public void quack() { System.out.println("Quack!"); }
}

public class Squeak implements QuackBehavior {
    public void quack() { System.out.println("Squeak!"); }
}

// 3. The Duck uses the behavior (Composition)
public abstract class Duck {
    QuackBehavior quackBehavior; // This is the encapsulation

    public void performQuack() {
        quackBehavior.quack(); // Delegate the work
    }

    public void setQuackBehavior(QuackBehavior qb) {
        this.quackBehavior = qb;
    }
}
```

## Program to an Interface, Not an Implementation

when you create an instance/object create it for an interface

### violation 

When you write `ColVert c = new ColVert();`, you are "locking" your variable `c` to only ever be a Mallard (ColVert).

If you later decide that this variable should sometimes be a `Plastique` (Rubber Duck), you have to go back through your code and change the data type everywhere. In a large project, this is a nightmare.

### solution

**with interface as type and later on decide its intialization**

```Java
// We don't care what SPECIFIC duck it is, as long as it's a Duck.
Canard myDuck;

if (userWantsRealDuck) {
    myDuck = new ColVert();
} else {
    myDuck = new Plastique();
}

// This line works regardless of what happened above!
myDuck.cancane();
```

**or create it with a method(like static method)**

```Java
public class DuckSimulator {
    
    public void runSimulation() {
        // We call a method to get "some kind of duck"
        Canard a = DuckFactory.createDuck(); 
        
        // This code NEVER has to change, even if we add 100 new duck types
        a.cancane();
    }
}
```

## Favor Composition over Inheritance 

- **Inheritance** breaks encapsulation.
- **Composition** is defined dynamically.

### Example

![[image-304.png]]

```Java
public interface MoveBehavior {
    void move();
}

public class Walk implements MoveBehavior {
    public void move() { System.out.println("Walking on the ground."); }
}

public class Fly implements MoveBehavior {
    public void move() { System.out.println("Flying through the air!"); }
}

public class Teleport implements MoveBehavior {
    public void move() { System.out.println("Zapping to a new spot."); }
}

public abstract class Actor {
    // Composition: Actor HAS-A MoveBehavior
    protected MoveBehavior moveBehavior;

    public void performMove() {
        moveBehavior.move(); // Delegation
    }

    public void setMoveBehavior(MoveBehavior mb) {
        this.moveBehavior = mb;
    }
}
```




