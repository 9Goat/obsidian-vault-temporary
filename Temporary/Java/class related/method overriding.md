method overriding is when we write a method inside a subclass that matches a method in the extended parent class ,this is useful when we wan to write a modified version of the method in the subclass.

# Syntax

```Java
class parentClass{
returnType methodName(parameters){
    // method body
}
}

class subclass extends parentClass{
    @Override
    returnType methodName(parameters){
        // overridden method body
    }
}
```

- **`returnType`**,**`methodName`** , **`access modifiers`** and **`parameters`** inside the override method **MUST** match  the extended parent class to work as intended
- the override method has a higher priority than the extended method meaning when we call the method from an object of the sub class it will execute the overridden method instead of the parent class method.

# @Override


this **`@Override`** keyword is **OPTIONAL** it is used to make sure the method we are trying to overriding is actually overridden buy showing an error or warning if the method doesn't exist in the parent class or if the method is **NOT** correctly declared (e.g., different return type, method name, or parameters).

# Example

```Java
public class methodOverridingInJava {
    public static void main(String args[]){
        student Student = new student("Ilyes");
        Student.presentYourself(); 
    }
}
class person{
    String name;
    person(String name){
        this.name = name;
    }
    void presentYourself(){
        System.out.println("Hello my name is "+name);
    }
}

class student extends person{
    student(String name){
        super(name);
    }
    @Override
    void presentYourself(){
        System.out.println("Hello my name is "+name+" and iam a Student");
    }
}
```

# Notes

- it is possible to have more than 1 override method inside a class as long as each one of them is valid
- override only works with [[Temporary/Java/class related/inheritance|extended]] methods 
- the **`@Override`** keyword **MUST** my written exactly above the method we are overriding with for it to work as intended

