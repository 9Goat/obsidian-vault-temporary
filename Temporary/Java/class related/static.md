static is a keyword that is used to declare a variable or method as a class variable or method, meaning it belongs to the class itself, rather than instances of the class.

# Syntax

```Java
class ClassName {
    // static variable
    static dataType variableName = value;

    // static method
     static returnType methodName(parameterList) {
    // method body
}
}
```

# How it works

- when we create an [[Methods & Objects#Objects|object]] all variables and methods information and attached to that object (*for example if we change the value of an instance variable in one object, it doesn't affect the value of the same variable in another object*). 
- **BUT** with static variables and methods **ALL** objects of the class share the same copy , meaning if we change the value of a static variable the change will be applied to **ALL** objects

## Example 1

```Java
// SimpleStaticDemo.java
class SharedValue {
    static int commonNumber = 0; // This variable is shared by ALL objects

    public static void main(String[] args) {
        System.out.println("Initial commonNumber: " + SharedValue.commonNumber); // 0

        SharedValue obj1 = new SharedValue();
        SharedValue obj2 = new SharedValue();

        obj1.commonNumber = 5; // obj1 changes the shared variable
        System.out.println("obj2 sees commonNumber: " + obj2.commonNumber); // Output: 5 (obj2 sees the change)

        SharedValue.commonNumber = 10; // Change directly via class name
        System.out.println("obj1 sees commonNumber: " + obj1.commonNumber); // Output: 10 (obj1 sees the change)
    }
}
```

- to access a static variable or method it is **RECOMMENDED** to call it using the class name but it is *possible* to call it via the object name like instance variables and methods.

## Example 2

```Java
public class MyClass {
    static int staticVar = 10; // Static variable
    static void staticMethod() { // Static method
        System.out.println("Static method called.");
    }

    public static void main(String[] args) {
        // RECOMMENDED: Access using the Class Name
        System.out.println("Via Class Name: " + MyClass.staticVar);
        MyClass.staticMethod();

        // POSSIBLE (but NOT recommended): Access using an Object Name
        MyClass obj = new MyClass();
        System.out.println("Via Object Name: " + obj.staticVar);
        obj.staticMethod();
    }
}
```

- any changes made to a static method will be saved to **ALL** objects of that static method

## Example 3

```Java
// SimpleStaticMethodChange.java
class AppConfig {
    static String theme = "Light"; // Shared static variable

    // Static method to change the shared static variable
    public static void setTheme(String newTheme) {
        theme = newTheme;
    }

    public static void main(String[] args) {
        System.out.println("Initial theme: " + AppConfig.theme); // Light

        AppConfig user1 = new AppConfig();
        AppConfig user2 = new AppConfig();

        AppConfig.setTheme("Dark"); // Static method changes the shared 'theme'

        System.out.println("User 1 sees theme: " + user1.theme); // Output: Dark
        System.out.println("User 2 sees theme: " + user2.theme); // Output: Dark
    }
}
```
# Example

```Java
public class Students{
    static int counter = 0;
    String name;

    Students(String name){
        this.name = name;
        counter++;
    }

    public static void main(String[] args){
        Students student1 = new Students("Ilyes");
        Students student2 = new Students("Sarra");
        Students student3 = new Students("Eya");
        
        System.out.println(Students.counter);
    }
}
```

# Notes

- we **CANNOT** call non static methods inside static methods

and the reason why its possible with non static is that when we call the non static method inside the non static method we are passing the keyword [[this]] inside. which is basically saying Hey, *this object (the one I'm currently operating on) should also perform this other action* . **BUT** with static methods we dont know for which object we are operating for which is why we cannot call a non static method

