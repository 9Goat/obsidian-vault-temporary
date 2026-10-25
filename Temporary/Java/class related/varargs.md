the varargs or *variable arguments* are use to create methods and constructors that can accept any number of parameters of the same datatype without having to create many methods that use [[Method overloading]]

# Syntax

to create a varargs of parameters you need to add ellipsis `...` (*3 dots*) between the datatype and the name of the parameter.


```Java
returnDatatype methodName(datatype... variableName){
//statements or block of code to be executed
}
```

# Explanation

when we call the varargs method, we can pass **ANY** number of arguments of *that datatype* (including zero arguments) to the method. when the method received our parameters it will automatically store them in an array.

## Example

```Java
sum(1,2,3,4,5); //any number of parameters is accepted as long they are the same type

int sum(int... numbers){
// numbers --> array of {1,2,3,4,5}
//statements here
}
```

# Calling a method with args

there are 3 ways to pass arguments to a varargs method.

## With a comma-separated list of arguments

```Java
printNames("Alice", "Bob", "Charlie");
```

## With an array

```Java
String[] myNames = {"David", "Eva"};
printNames(myNames);
```

## With no arguments

```Java
printNames();
```

# Example 

```Java
public class Calculator {
    
    public int sum(int... numbers) {
        int total = 0;
        for (int number : numbers) {
            total += number;
        }
        return total;
    }

    public static void main(String[] args) {
        Calculator calc = new Calculator();
        
        // Passing a few arguments
        System.out.println("Sum of 1, 2, 3: " + calc.sum(1, 2, 3)); 
        
        // Passing an array
        int[] myNumbers = {10, 20, 30, 40};
        System.out.println("Sum of array elements: " + calc.sum(myNumbers));
        
        // Passing no arguments
        System.out.println("Sum with no arguments: " + calc.sum());
    }
}
```
# Notes

- inside the method itself we **MUST** treat the [[varargs]] as an array (*by using [[Arrays in java#Displaying arrays with enhanced for-loop|for loops]] for example*)
- you can only have **ONE** [[varargs]] per method
- it is possible to pass normal arguments alongside the [[varargs]] as long as the [[varargs]] is the **LAST** parameter within the method
	- **Example**: `methodName(datatypes otherParameters, datatype... variableName)`
