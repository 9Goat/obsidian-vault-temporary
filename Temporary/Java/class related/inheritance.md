inheritance is the act of providing variables and methods from a parent class to a child class using the `extends` keyword in Java. This is useful when we want to reuse code from a class that shares the same traits with a child class

# Syntax

```Java
class parentClass{
//variables and methods
}

class childClass extentds parentClass{
// all variables and methods from parentClass are accessible here as well
}
```

# Example

```Java
public class TryingInheritanse{
public static void main(String args[]){
    cat newCat = new cat(14,"Garfield");

    newCat.meow();
}
}
class livingBeing{
    boolean isAlive = true;
}

class animal extends livingBeing{
    int age;
    String name;
}

class cat extends animal{
    void meow(){
        if (isAlive)
        System.out.println("meow my name is "+name+" and iam "+age+" years old!");
    }
    cat(int age,String name){
        this.age = age;
        this.name = name;
    }
}
```

# Notes

- we can only have a **SINGLE** extends for each class 
- with extends we can create relationships between class like this for the example above
	- livingBeing -> animal -> cat, where `->` represents inheritance.

