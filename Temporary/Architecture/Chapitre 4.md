
# Design pattern definition

it can be described in 2 things: 

- **A problem** that happens over and over again in a specific environment.
- **The architecture of the solution** to that problem, designed so that you can reuse it thousands of times without ever doing the same thing twice.

**in short**

A **design pattern** is a reusable **"blueprint"** used to solve a common problem that keeps coming up in software design,.

# Advantages of design patterns

- **Proven Solutions:** You use methods that are already tested and known to work.
- **Big Picture View:** You look at how the whole system fits together, not just small pieces of code.
- **Shared Language:** Developers can talk to each other much faster using common terms.
- **Built-in Manual:** They help explain how the software is structured.
- **Handles Hard Projects:** They make it easier to build complex and difficult apps.

# Types of design patterns

design patterns can be split into 3 main categories which are the following:

- **Creational Patterns:** These patterns are all about **how you create objects**. Instead of just randomly making objects everywhere, these patterns give you a strict way to "manufacture" them.. (Examples: Abstract Factory, Builder, Prototype, Singleton).
	- **Simple Goal:** Making sure objects are created and set up correctly without the rest of the app needing to know the "how".

- **Structural Patterns:** These focus on **connecting objects** together so that the connections can handle future changes easily. (Examples:Adapter(objet), Composite, Bridge, Decorator, Facade, Proxy).
	- **Simple Goal:** Connecting objects in a way that makes it easy to change or add new parts later without breaking everything.

- **Behavioral Patterns:** These focus on how objects **interact and talk** to each other. (Examples: Strategy, Observer, Iterator, Mediator ,Visitor, State).
	- **Simple Goal:** Organizing the communication and "behavior" between different parts of the app.

# Levels of design patterns

design patterns either focus on classes or objects

- **Class Scope:** Focuses on relationships between classes and their subclasses using **inheritance**.
- **Instance (Object) Scope:** Focuses on relationships between individual objects using **composition**.

# Components of design patterns

Every design pattern is described using four essential elements.

1. **Name:** A word or two used to identify the pattern, its solution, and its effects. 
2. **Problem:** This describes **when** to apply the pattern. It explains the specific trouble you're facing and the context or situation where this pattern is the best fit.
3. **Solution:** This describes **how** the solution is built. It shows the "parts" (objects, relationships, and responsibilities) and how they work together, often using diagrams to show how they behave.
4. **Consequences:** This describes the **results** of using the pattern. It's very important because it lists both the **positive and negative effects** on your system so you can decide if the trade-off is worth it.

# Requirements of every IT project

1. **Functional Requirements (The "What")**
	- They describe the specific tasks the software must do for the user.
	- **Example:** In a banking app, a functional requirement is "the user must be able to transfer money to another account".
2. **Technical Requirements (The "How")**
	- They don't focus on what the user does, but on how the system handles the work. These ensure the app is reliable, safe, and works on different devices.
	- **Examples:**
		- **Performance:** The app must load quickly.
		- **Security:** User data must be encrypted.
		- **Portability:** The app must work on both a computer (Desktop) and a phone (Mobile).
3. **Financial Requirements (The "Cost")**
	- This is the business side of the project. Every piece of software has a limit on how much money can be spent to build it.
	- **Example:** The project must be completed using only the $50,000 budget assigned to the department.

# The benefits of using OOP

- **Reuse proven solutions** (like Design Patterns) so we don't have to reinvent the wheel.
- Create applications that are **easy to maintain** , **secure** and **fast** .
- **Separate different parts** of the application so that changing one thing doesn't break everything else.

# Inheritance vs composition

## 1. Inheritance (The "Is-a" Relationship)

This is when one class is a **special version** of another class. The child class "inherits" everything from the parent.

- **Key phrase:** "Is a" or "A kind of".
- **Code clue:** You will see the word `extends` (for example, `class B extends A`).
- **Simple Example:** A **Car** "is a" **Vehicle**. A **Cat** "is an" **Animal**.

## 2. Composition (The "Has-a" Relationship)

This is when one class **uses** another class by keeping a piece of it inside. Instead of being a version of that class, it just "owns" or "has" an instance of it.

- **Key phrase:** "Has a" or "Has many".
- **Code clue:** You will see one class creating an object of another class inside it (for example, `class C { A a = new A(); }`).
- **Simple Example:** A **Car** "has an" **Engine**. A **House** "has a" **Room**.

![[image-349.png]]

# Summary

- a design pattern can be described as a **solution** blueprint to a **problems** that are related to software design
- the advantages of design patterns are:
	- they are proven to be correct
	- it describes an entire component of the program, not a part of it(meaning the structure not a single code file)
	- easier communication, since those design patterns are known they can be used to explain software designs
	- they make maintaining and creating complex projects easier
- there are 3 main types of design patterns which are:
	- **creational**: focus on how the classes are create
	- **Structural**:focuses on how the classes are connected with each other, so its easier to add more to the structure
	- **behavioral**: focuses on how the classes interact with each other 
- each design pattern either focuses on:
	- **classes** with inheritance
	- **objects** with compositions
- each design pattern has the following:
	- name
	- a problem to solve
	- solution
	- consequences (either positive or negative)
- each it project has 3 requirements to be successful which are:
	- **functinoal requirements**: describes how the user will be interacting with the project
	- **technical requirements** describes how the system will function
	- **financial requirements** the budget of the project
- benefits of using OOP with design patterns:
	- resuable solutions
	- easier to maintain and improve (fast and secure)
	- separated, meaning if we change something it wont break other parts of the project
- inheritance vs composition
	- in inheritance we say that a class is a type of an another class and we use extend to use its funcionalities
	- in composition we say that a class has an another object of a class and we use new object() to access the funcionalities of that class
