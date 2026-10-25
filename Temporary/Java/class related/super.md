super is used to access [[Temporary/Java/class related/inheritance|extended]] classes 

# Syntax

```Java
class parentClass{

//parentClass constructor
parentClass(parameters){
// variables intialization
}
}

class childClass extends parentClass{

//childClass constructor
childClass (parameters){
super(parameters);
// variables intialization
}
}
```

- with the `super` keyword we are accessing the constructor of the parent class, and providing the same required parameters as parentClass constructor
- the reason why we do this is because you **CANNOT** use [[Constructors]] to initialise [[Temporary/Java/class related/inheritance|extended]] variables from a parentClass
	- **for example This is false**

```Java
class childClass extends parentClass{

//childClass constructor
childClass (parameters){

this.parentClassObjectVarible = parameterFromParentClass;
}
}
```

- [[super]] can also be used to call methods or access fields from a parent class, just like the  keyword [[this]]

## Example1

```Java
public class SuperMethodExample {
    public static void main(String[] args) {
        Dog myDog = new Dog();
        myDog.makeSound(); // Calls the Dog's makeSound, which then calls Animal's makeSound
    }
}

class Animal {
    void makeSound() {
        System.out.println("Animal makes a sound.");
    }
}

class Dog extends Animal {
    @Override
    void makeSound() {
        super.makeSound(); // Calls the makeSound method from the Parent (Animal) class
        System.out.println("Dog barks.");
    }
}
```
# Example

```Java
public class SuperConstructorExample {
    public static void main(String[] args) {
        Child myChild = new Child(100);
        System.out.println("Value from parent: " + myChild.value);
    }
}

class Parent {
    int value;

    Parent(int value) {
        this.value = value;
        System.out.println("Parent constructor called with value: " + value);
    }
}

class Child extends Parent {
    Child(int value) {
        super(value);
        System.out.println("Child constructor called.");
    }
}
```


# Notes

- it is possible to have multiple super to access multiple constructors of a parent class
- super **MUST** be the first statement inside the child class constructor otherwise we will get an error
- super **ONLY** works when inside a subclass that has a parent class extended to it
