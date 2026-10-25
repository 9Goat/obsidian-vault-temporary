interfaces are used to [[Temporary/Java/class related/inheritance|inherit]] multiple [[abstract]] classes by using the keyword **`implements`**

# Syntax

```Java
interface parentClass{
//methods and variables declaration here
}

class childClass implements parentClass1. parentClass2, ...{
@Override
//override all the methods declared within the interface for it to work
}
```
# Example

```Java
public class interfacesInJava {
    public static void main(String[] args) {
        Dog dog = new Dog("chiwawa",14,14.8);
        dog.walk();
        dog.makeSound();
        dog.hunt();
    }
}

interface Animal{
    //all variables declare inside the interface are static,final and public
    boolean isAlive = true;

    //methods inside interfaces are public and abstract
    void makeSound();
}

interface Walkable{
    void walk();
}

interface Hunter{
    void hunt();
}

class AnimalInformation{
    int age;
    double length;
    AnimalInformation(int age,double length){
        this.age = age;
        this.length = length;
    }
}

class Dog extends AnimalInformation implements Animal,Walkable,Hunter{
    String type;
    Dog(String type,int age,double length){
        super(age, length);
        this.type = type;
    }

    @Override
    public void makeSound(){
        System.out.println("the dog is making a sound WOOF WOOF");
    }

    @Override
    public void walk(){
        System.out.println("The dog is running");
    }

    @Override
    public void hunt(){
        System.out.println("The dog is hunting");
    }
}
```

# Notes

- interface classes and methods are by default [[abstract]] and **public** meaning we **MUST** [[method overriding|override]] the methods inside the child class with the same **public** [[Methods & Objects#Methods|Method]]
- we can implements multiple [[interfaces]] by separating them with a **comma** `,`
- interfaces variables are by default **[[Temporary/Java/class related/static]]**, **final** and **public**
- it is possible to use both [[Temporary/Java/class related/inheritance|extends]] and **implements** at the same child class 
	- we use interfaces to implement methods and we use [[Temporary/Java/class related/inheritance]] to extend variables this is the way we use both of them

## Example 1

```Java
class Duck extends Animal implements Swimmer {
    Duck(String name){
    super(name);
    }

    @Override
    public void swim() {
        System.out.println("Duck is paddling in the water.");
    }

    public void name() {
        System.out.println("My name is: " + name);
    }

    public static void main(String[] args) {
        Duck myDuck = new Duck("LeDuck");
        myDuck.swim();
        myDuck.name();
    }
}
class Animal {
    String name;
    Animal(String name){
    this.name = name;
    }
}

interface Swimmer {
    void swim();
}
```

