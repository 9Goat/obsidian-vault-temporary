just like in C arrays are used to store multiple values in a single variable, 

# Declaration

```Java
dataType[] arrayName;
// or
dataType arrayName[];
```

an array can be declared with any valid dataType in Java
# Initialization

there are 2 ways to create an array in java:

- arrays with predefined elements, where the size of the array is determined by the number of elements provided, and 
- arrays with a specified size, where the size is defined, and elements can be added or modified later.

## Arrays with predefined elements

in this version we are assigning values to the array at the time of declaration.the size of the array is determined by the number of elements were initialized.

### Syntax

``` Java
dataType[] arrayName = {element1, element2, ..., elementN};
// or
dataType arrayName[] = {element1, element2, ..., elementN};
//or
dataType arrayName[] = new dataType[] {element1, element2, ..., elementN};
```

### Example

```Java
public class arraysInJava {
    public static void main(String[] args){
        String [] fruits = {"Apple", "Banana", "Cherry", "Date"};
        for (String fruit : fruits) {
            System.out.println(fruit);
        }
        System.out.println("Length of the array: " + fruits.length);
    }
}
```

## Arrays without predefined elements

in this version we are specifying the length of the array while keeping the elements of the array empty

### Syntax

```Java
dataType arrayName = new dataType[size];
```

### Example

```Java
public class arraysInJava {
    public static void main(String[] args){
        String [] fruits = new String[3];
        fruits[0] = "Apple";
        fruits[1] = "Banana";
        fruits[2] = "Orange";
        for (String fruit : fruits) {
            System.out.println(fruit);
        }
        System.out.println("Length of the array: " + fruits.length);
    }
}
```

# Displaying arrays with enhanced for-loop

unlike other languages like python the only way to display arrays is to go through all of their elements one by one using a [[Things that are the same in C#for loops|for loops]] Thankfully java offers an enhanced for loop (*for-each*) that works perfectly for arrays

## Syntax

```Java
for (dataType elementName : arrayName) {
    // Code to execute for each element
}
```

- **`elementName`** : a variable name we choose to represent each element in the array during each iteration of the loop.

## Example

```Java
public class arraysInJava {
    public static void main(String[] args){
        int [] numbers = {1, 2, 3, 4, 5};
        for (int number : numbers) {
            System.out.println(number);
        }
    }
}
```

## Note

- the local variable we are using for each array element inside enhanced for loop can **ONLY** access the value of the element and **NOT** modify it,if you want to modify the value of elements use the standard [[Things that are the same in C#for loops|for loops]] instead
# Determining the length of an array

java offers a built-in method to determine the length of an array

## Syntax

```Java
int variable = arrayName.length;
```

## Example

```Java
public class arraysInJava {
    public static void main(String[] args){
        int [] numbers = {1, 2, 3, 4, 5};
        int lengthOfArray = numbers.length;
        System.out.println("Length of the array: " + lengthOfArray);
    }
}
```

# Things that are the same as C arrays

## Accessing elements

you access elements by writing the index of the element you want to access in square brackets after the array name. **` arrayName[index]`**.

### Example

```Java
public class ArrayAccessExample {

    public static void main(String[] args) {
        int[] numbers = {10, 20, 30};

        System.out.println(numbers[0]);
        System.out.println(numbers[1]);
    }
}
```

## Multidimensional Arrays

Just like C, Java also supports multidimensional arrays, which are arrays of arrays.

### Example

```Java
public class MultiDimArrayAccessExample {

    public static void main(String[] args) {
        int[][] matrix = {{1, 2}, {3, 4}};

        System.out.println(matrix[0][0]); // Accesses 1
        System.out.println(matrix[1][1]); // Accesses 4
    }
}
```

**OR to create a multidimensional arrays with specified size**

**`dataType[][] arrayName = new dataType[numberOfRows][numberOfColumns];`**

