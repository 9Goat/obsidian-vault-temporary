generics allow us to make a method or a class functional for all object types

# problem

```Java
public class GenericsTest {  
public static void main(String[] args) {  
	int i = 5;  
	String s = "hello";  
	VariablePrinter v = new VariablePrinter();  
	v.printVariable(i); 
	v.printVariable(s); //this will result in an error 
}}  

class VariablePrinter{  
	//method that only works integers  
	public void printVariable(int x){  
	System.out.println(x);  
}  
}
```

the problem with this code is that if we want to print the string we would have to create a separate method just for string which would result in code duplication

# Solution

we can add generics! instead of specifying a certain datatype like int we could instead use a an object placeholder that plays the role of all objects

```Java
public class GenericsTest {  

public static void main(String[] args) {  
//int i = 5; since T is an object holder we need to use Integer(classwrapper)  
Integer i = 5;  
String s = "hello";  
VariablePrinter v = new VariablePrinter();  
v.printVariable(i);  
v.printVariable(s);  

}}  

class VariablePrinter{  
//method that only works integers  
public <T> void printVariable(T x){  
System.out.println(x);  
}}
```

# Generic methods

## Syntax

```Java
[access modifier/static] <genrics> return-type methodName(parameters){
//statements
}
```

- the generics can be multiple generics not just a single one
	- **Example**: <T,U,V> void method(T var1, U var2, V var3) 3 generics
- the return type can be a generic too
	- **Example**: `public <T> T returnT(T variable)`
- also the parameters types can also contain generics just like the example above
- generics only works with objects not datatypes meaning we have to convert them to objects using [[Wrapper class]]

## Example

```Java
public class GenericExample {

    // This is a generic method. 
    // <T> is a type parameter that represents any object type.
    public static <T> void printArray(T[] elements) {
        for (T element : elements) {
            System.out.print(element + " ");
        }
        System.out.println();
    }

    public static void main(String[] args) {
        // Create arrays of different types
        Integer[] intArray = {1, 2, 3, 4, 5};
        String[] stringArray = {"Hello", "Generics", "are", "cool"};
        Double[] doubleArray = {1.1, 2.2, 3.3};

        System.out.println("Printing Integer Array:");
        printArray(intArray);

        System.out.println("Printing String Array:");
        printArray(stringArray);

        System.out.println("Printing Double Array:");
        printArray(doubleArray);
    }
}
```

# Generic class

instead of methods we can also create classes and objects that store different types of data

## Syntax

```Java
[access modifier/abstract or interface] class className <generics>{
//statements
}
```

- just like generic methods we can specify multiple generics instead of a single one

## Example

```Java
public class GenericsTest {  
public static void main(String[] args) { 
 
Integer i = 5;  
String s = "hello";  

Variable<Integer> integerVariable = new Variable<>(i);  
integerVariable.printVariable();  
Variable<String> stringVariable = new Variable<>(s);  
stringVariable.printVariable();

}  
}

class Variable<T>{  

T ourVariable; 
 
Variable(T x){  
ourVariable = x;  
}  

public void printVariable(){  
System.out.println(ourVariable);  
}  

}
```

## Notes

- for the class the type of generics we specify in the generalization does **NOT** change the class itself
	- **Examples**: lets say we create a generic class and put integer in it and another for string if we compare them with `return stringVariable == integerVariable` this will return **TRUE** meaning the  generics dont differentiate to the class they view  them all the same(***this also applies to static, it applies to ALL instances***)

## Inheritance

### inheritance on the generics themselves

we can restrict the number of classes that we allow by specifying inheritance on a generic

```Java
class className <T extends U> {
//statements here
}
```

this tells the compiler ***T must be either the class U itself OR one of its subclasses***

for example if instead of U we wrote Person then it will only accept either a person class or one of its subclasses like student

**Note**:
- it is possible to add more options of extend (specification) by separating them with `&` this tells the compiler that this class must also implements the interfaces that are after `&` (**The first extends refers to class the ones after are considered interfaces**)
	- **Example**

```Java
public class Garage {
    // T must be a Vehicle AND implement Electric AND implement Autonomous
    public <T extends Vehicle & Electric & Autonomous> void serviceSmartCar(T car) {
        car.drive();          // From Vehicle
        car.chargeBattery();  // From Electric
        car.startAutoPilot(); // From Autonomous
    }
}
```

### inheritance from a generic class

when we inherit a generic class we **MUST** specify the names of the generics used on that extended class

**Example** : this examples shows a class that only inherits a specific type of generic

```Java
public class Box<T> {
    private T item;
}

// Subclass specifies "String" as the type
public class StringBox extends Box<String> {
    // This class now specifically handles Strings
}
```



**Example**: this example shows a class that accepts any type of inheritance

```Java
// Base Generic Class
class Container<T> {
    T item;

    public Container(T item) {
        this.item = item;
    }

    public T getItem() {
        return item;
    }
}

// Subclass inheriting from Container
// We pass the type 'T' up to the parent
class SpecialContainer<T> extends Container<T> {
    
    public SpecialContainer(T item) {
        super(item);
    }

    public void printInfo() {
        System.out.println("Stored item: " + getItem());
    }
}

public class Main {
    public static void main(String[] args) {
        // SpecialContainer inherits the logic from Container
        SpecialContainer<String> nameBox = new SpecialContainer<>("Gemini");
        nameBox.printInfo();

        SpecialContainer<Integer> ageBox = new SpecialContainer<>(25);
        ageBox.printInfo();
    }
}
```

**Note**:

- when we extend the parent class and make its generic fixed like **String** then we can remove the generic symbol from the child
- otherwise if we want to keep the parent class generic not fixed we **MUST** keep the generic symbol on the child meaning
	- `class SpecialContainer extends Container<T>` is incorrect (because the compiler has no idea that T could be, lets say we want to use a method from the parent that uses the generic T, what would be provide for that method? we dont even know what T is)
- in class inheritance we cant make the parent class specific by using extend that will result in a compile error

![[image-312.png]]

- while we cant make a non generic class inherit a generic  class, the opposite is true if the parent class is **NOT** generic but the child class is we can still extend it