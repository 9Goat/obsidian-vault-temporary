most datatypes inside of java are similar to C programming that is why i wont be explaining them in details

# numerical datatypes

From the smallest to the largest :

## non float numbers

### Byte

 signed byte meaning it ranges from `-128` to `128` 

### Short

 signed **2** byte meaning it ranges from `-32k` to `32k` 

### Int

signed **4** byte meaning it ranges from `-2b` to `2b` 

### Long

signed **8** byte 

## Float numbers

### float

- has the same size as int
- it allows up to 7 decimal digits of precision (digits behind the float point)
- you have to add the letter `f` at the end of a float number to be treated as such otherwise we will get a conversion error because decimal point numbers automatically get converted to double instead of float
	- **Example** : `3.14f`

### Double

- same size as long
-  it allows up to 16 decimal digits of precision (digits behind the float point)

## Example

```Java
public class testingVariables {

public static void main(String[] args) {

byte b = 100;

short s = 20;

int i = 30;

long l = 40;

float f = 50.5f;

double d = 60.6;

// Printing the variables

System.out.println("Byte: " + b + "\n");

System.out.println("Short: " + s + "\n");

System.out.println("Integer: " + i + "\n");

System.out.println("Long: " + l + "\n");

System.out.println("Float: " + f + "\n");

System.out.println("Double: " + d + "\n");

}

}
```

# Character related datatypes

## Char 

same as C but it takes 2 bytes instead of 1

## String

string is not a datatype like the others but instead a class in the java.lang package when you create a string variable you are creating an object not a variable

- once you create a string object you cannot modify its value
- trying to change the value of the string will result in creating a new string object with the new value and assign it to that variable while keeping the old variable value stored in the memory garabage

## Example

```Java

public class testingVariables {

public static void main(String[] args) {

char c = 'c';

String str = "Hello, World!";

// Printing the variables

System.out.println("Character: " + c + "\n");

System.out.println("String: " + str + "\n");

}}
```

# Boolean datatype

boolean in  a bit  different compared to C in a sense that you cannot convert int values of `1` or `0` to **True** or **False** 

- the default value of Boolean is `false`
- the only values you can assign to boolean are :
	- `true`
	- `false`
	- anything else will return an error

## Example

```Java

public class testingVariables {

public static void main(String[] args) {

boolean bool = true;

// Printing the variables

System.out.println("Boolean: " + bool + "\n");

}}
```