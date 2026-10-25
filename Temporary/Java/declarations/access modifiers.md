access modifiers determines which classes can access a particular variable or method of class

keywords to be aware of in this note:

- **package** : means they are within the directory
- **sub class**: means they are a child class from a parent class using the [[Temporary/Java/class related/inheritance]]

# Types of access modifiers

there are 4 main types of access modifiers which are:

- public
- private
- protected
- package/default/friendly

## Private

The private access modifier is specified using the keyword private. The methods or data members declared as private are accessible **only** within the class in which they are declared.

### Example

```Java
class MyClass {
    private String secretData = "This data is private."; // private variable

    public void revealSecret() {
        // This method can access secretData because it's within the same class
        System.out.println(secretData);
    }
}

public class PrivateAccessDemo {
    public static void main(String[] args) {
        MyClass obj = new MyClass();
        obj.revealSecret(); // This works because revealSecret() is public

        // The following line would cause a compile-time error:
        // System.out.println(obj.secretData);
        // Error: 'secretData' has private access in 'MyClass'
    }
}
```

## Public

The public access modifier is specified using the keyword public. Public members are accessible from everywhere in the program. There is no restriction on the scope of public data members.

### Example

```Java
class MyPublicClass {
    public String publicData = "This data is public."; // public variable

    public void displayPublicData() {
        // This method is public and can be called from anywhere
        System.out.println("Inside MyPublicClass: " + publicData);
    }
}

public class PublicAccessDemo {
    public static void main(String[] args) {
        MyPublicClass obj = new MyPublicClass();

        // Accessing the public variable directly from another class
        System.out.println("Accessed directly: " + obj.publicData);

        // Calling the public method from another class
        obj.displayPublicData();
    }
}
```

## Protected

The protected access modifier is specified using the keyword protected. The methods or data members declared as protected are accessible within the same package or subclasses in different packages.

you simple use the keyword **`protected`** before the variable name(we cannot show an example since a package visibility difference CANNOT be shown in a single code file.)

## Package/default

When no access modifier is specified for a class, method, or data member, it is said to have the default access modifier by default. This means only classes within the same package can access it.

### Example

```Java
// MyDefaultClass.java
class MyDefaultClass {
    // No access modifier specified, so 'defaultData' has package-private access
    String defaultData = "This data has default (package-private) access."; 

    // No access modifier specified, so 'displayDefaultData' has package-private access
    void displayDefaultData() { 
        System.out.println("Inside MyDefaultClass: " + defaultData);
    }
}

// DefaultAccessDemo.java
public class DefaultAccessDemo {
    public static void main(String[] args) {
        MyDefaultClass obj = new MyDefaultClass();

        // We can access 'defaultData' and 'displayDefaultData()' directly
        // because MyDefaultClass and DefaultAccessDemo are in the same package.
        System.out.println("Accessed directly from DefaultAccessDemo: " + obj.defaultData);
        obj.displayDefaultData();
    }
}
```

# Conclusion

![[image-35.png]]