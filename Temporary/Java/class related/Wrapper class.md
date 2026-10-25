a wrapper class is the action of turning a primitive [[Basic datatypes]] into an object

Java provides a set of wrapper classes in the `java.lang` package, which is imported automatically. There is a specific wrapper class for every primitive data type:

| **Primitive** | **Wrapper Class** |
| ------------- | ----------------- |
| `byte`        | `Byte`            |
| `char`        | `Character`       |
| `int`         | `Integer`         |
| `double`      | `Double`          |
| `boolean`     | `Boolean`         |
- [[Basic datatypes#String|String]] does not have a wrapper since it is be default an object
# Why Wrapper Classes Are Needed

Wrapper classes are required in Java for the following reasons:

- Java collections (ArrayList, HashMap, etc.) store only objects, not primitives.
- Wrapper objects allow primitives to be used in object-oriented features like methods, synchronization, and serialization.
- Objects support null values, while primitives do not.
- Wrapper classes provide utility methods such as compareTo(), equals(), and toString().

# Syntax

there are 2 syntax for wrapper classes which are boxing and unboxing

- **Boxing:** Converting a primitive to a wrapper object.
- **Unboxing:** Converting a wrapper object back to a primitive.


```Java
//boxing
wrapperClass ObjectName = value;
//unboxing
datatype variableName = objectName;

//for example

// Autoboxing: int to Integer
Integer myObject = 10; 

// Auto-unboxing: Integer to int
int myPrimitive = myObject;

```





