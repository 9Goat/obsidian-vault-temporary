the array class is used to modify and manipulate arras in java

# Syntax

**`import java.util.Arrays`**

# Methods 

unlike other classes we dont need to create an object of that class to access its methods

## Syntax

**`Arrays.methodName(parameters //usually just the arrays name)`**

## Sort method

is used to sort the elements of an array from **lowest** to **highest** it works on all primitive [[Basic datatypes]]

### Syntax

`Arrays.sort(arrayName,firstIndexToSort,LastIndexToSort);`

- **`firstIndexToSort` (OPTIONAL)** :  is **INCLUSIVE**, meaning it starts sorting from this index
- **`LastIndexToSort` (OPTIONAL)** is **EXCLUSIVE**, meaning it stops sorting before this index.


### Example

#### Example without indexes

```Java
import java.util.Arrays;

public class ArraySortExample {

    public static void main(String[] args) {
        int[] numbers = {5, 2, 8, 1, 9};
        Arrays.sort(numbers); // Sorts the array in ascending order
        System.out.println(Arrays.toString(numbers)); // Output: [1, 2, 5, 8, 9]
    }
}
```

#### Example with indexes

```Java
import java.util.Arrays;
public class arraysInJava {
    public static void main(String[] args){
    int[] numbers = {5, 2, 8, 1, 9, 4, 7, 3, 6};

        System.out.println("Original array: " + Arrays.toString(numbers));

        // Sort a portion of the array from index 2 (inclusive) to 6 (exclusive)
        // This means elements at index 2, 3, 4, 5 will be sorted.
        // The elements are {8, 1, 9, 4}
        Arrays.sort(numbers, 2, 6);

        System.out.println("Array after sorting from index 2 to 6: " + Arrays.toString(numbers));
    }
}

```

### Notes

- the sort method does **NOT** work with boolean arrays
- for strings arrays the way the sort method work is:
	- it firsts compare the first letter of each string based on which one has the lower unicode to pick if they are the same it moves to the next letter
	- if one string is **shorter** than the other it will be picked
- if we specify the indexes we **MUST** specify both indexes, trying to specify just one will result in a compiler error
- the starting index **MUST** be smaller or equals to the ending index

## Binary Search Method

The binary search method is used to find the index of a specific element in a **SORTED** array

### Syntax

`binarySearch(arrayName, fromIndex, toIndex, valueToFind)`

- just like [[Temporary/Java/imports/Arrays#Syntax|sort method]] the fromIndex is **INCLUSIVE** and the toIndex is **EXCLUSIVE**

### Example


```Java
import java.util.Arrays;
public class arraysInJava {
    public static void main(String[] args){
    int[] numbers = {10, 20, 30, 40, 50, 60, 70, 80, 90};

        // The array MUST be sorted for binary search to work correctly
        System.out.println("Sorted array: " + Arrays.toString(numbers));

        int key1 = 40;
        int index1 = Arrays.binarySearch(numbers, key1);
        System.out.println("Element " + key1 + " found at index: " + index1); // Expected: 3
        }}
```


### Notes

- for this method to work the array **MUST** be sorted (unsorted arrays wont give us an error but it will give is a wrong answer)
- when the key value being searched doesnt exist in the array we will get a negative value equals to
	- **`(the index where the value belongs inside the array * -1) + -1`**
#### Example

```Java
import java.util.Arrays;
public class arraysInJava {
    public static void main(String[] args){
    int[] numbers = {10, 20, 30, 40, 50};
        // Case 2: Value does not exist (smaller than smallest element)
        int notFoundIndex1 = Arrays.binarySearch(numbers, 5);
        System.out.println("Searching for 5: Index = " + notFoundIndex1); // Output: -1 (insertion point 0, so -(0)-1 = -1)

        // Case 3: Value does not exist (between existing elements)
        int notFoundIndex2 = Arrays.binarySearch(numbers, 25);
        System.out.println("Searching for 25: Index = " + notFoundIndex2); // Output: -3 (insertion point 2, so -(2)-1 = -3)

        // Case 4: Value does not exist (larger than largest element)
        int notFoundIndex3 = Arrays.binarySearch(numbers, 55);
        System.out.println("Searching for 55: Index = " + notFoundIndex3); // Output: -6 (insertion point 5, so -(5)-1 = -6)
    }
}
```

## Comparing methods

### equals method

the equal method is used to compare the content and length of two arrays. and it returns a boolean depending on whether the arrays are identical or not.

#### Syntax

`Arrays.equals(array1, array2)`

- it returns **True** if both `array1` and `array2` are equal otherwise it will return **False**

#### Example

```Java
import java.util.Arrays;
public class testingTheEqualsMethod {
    public static void main(String[] args) {
        int[] numbers1 = {10, 20, 30, 40, 50, 60, 70, 80, 90};
        int[] numbers2 = {10, 20, 30, 40, 50, 60, 70, 80, 90};
    if (Arrays.equals(numbers1,numbers2)){
        System.out.println("borh arrays are equals!");
    }
    else{
        System.out.println("both arrays are not equal!");
    }
    }
}
```

### deepEquals method 

is the same as [[Temporary/Java/imports/Arrays#equals method|equals method]] *except* that it **ONLY** works with multi dimensional arrays instead of the standard 1D array

#### Syntax

`Arrays.deepEquals(array1,array2);`

#### Example

```Java
import java.util.Arrays;
public class testingTheEqualsMethod {
    public static void main(String[] args) {
        int[][] array1 = {{1, 2}, {3, 4}};
        int[][] array2 = {{1, 2}, {3, 4}};
        int[][] array3 = {{1, 2}, {3, 5}};

        System.out.println("array1 and array2 are deep equal: " + Arrays.deepEquals(array1, array2));
        System.out.println("array1 and array3 are deep equal: " + Arrays.deepEquals(array1, array3));
    }
}
```

### compare method

used to compare 2 1D arrays that share the same datatypes one element by one element and it returns an  integer depending on the result

- **if arra1 > array2**: the compare method will return a positive number
- **if array1 < array2**: the compare method will return a negative number
- **if array1 == array2**: the compare method will return 0

#### Syntax

`Arrays.compare(array1,fromIndex1,toIndex1,array2,fromIndex2,toIndex2);`

- just like [[Temporary/Java/imports/Arrays#Sort method|sort method]] you can set the starting index and the ending  index for both arrays

#### Example

```Java
import java.util.Arrays;
public class testingTheEqualsMethod {
    public static void main(String[] args) {
        int[] arr1 = {1, 2, 3};
        int[] arr2 = {1, 2, 3};
        System.out.println("arr1 vs arr2: " + Arrays.compare(arr1, arr2)); // Output: 0

        int[] arr3 = {1, 2, 0};
        int[] arr4 = {1, 2, 3};
        System.out.println("arr3 vs arr4: " + Arrays.compare(arr3, arr4)); // Output: -1 (or any negative number)

        int[] arr5 = {1, 5, 3};
        int[] arr6 = {1, 2, 3};
        System.out.println("arr5 vs arr6: " + Arrays.compare(arr5, arr6)); // Output: 1 (or any positive number)
    }
}
```

#### Notes

the way this compare method work is:

1. if starts comparing each element of both arrays from first element to last element and if one element is different than the other it returns the  result
	-  if the datatypes of the arrays are [[Basic datatypes#String]] then each letters of an element will be compared to the other using their unicode
2. if all elements are equal it will check which array is longer and returns the result based on that.(longer array means greater)

### mismatch method

the mismatch method is  used to  compare 2 arrays and  return the index where a difference occurred otherwise if both arrays are identical it will return **-1**

#### Syntax

`Arrays.mismatch(array1,fromIndex1,toIndex1,array2,fromIndex2,toIndex2)`

- just like [[Temporary/Java/imports/Arrays#Sort method|sort method]] you can set the starting index and the ending  index for both arrays

#### Example

```Java
import java.util.Arrays;
public class testingTheEqualsMethod {
    public static void main(String[] args) {
        int[] array1 = {1,5,5,8};
        int[] array2 = {1,4,5,8};
        System.out.println("the first difference noticed between both arrays lays at the index: "+Arrays.mismatch(array1,array2));
        
    }
}
```

#### Notes

- if both arrays being compared are different in length and identical then the mismatch method will return the **length** of the shorter array

##### Example

```Java
import java.util.Arrays;
public class testingTheEqualsMethod {
    public static void main(String[] args) {
        int[] array1 = {1,5,5,8};
        int[] array2 = {1,5,5}; //shorter array (length = 3)
        System.out.println("the first difference noticed between both arrays lays at the index: "+Arrays.mismatch(array1,array2));
        
    }
}
```

## fill method

the fill method is used to change the values  of elements inside an array to a specific value within its parameters

### Syntax

`Arrays.fill(array,fromIndex,toIndex,value);`

- just like [[Temporary/Java/imports/Arrays#Sort method|sort method]] you can set the starting index and the ending  index for both arrays

### Example

```Java
import java.util.Arrays;
public class testingTheFillMethod {
    public static void main(String[] args) {
        int[] array1 = {14,6,89,4,2,3,8,6};
        Arrays.fill(array1,1,5,55);
        System.out.println(Arrays.toString(array1));
        
        Arrays.fill(array1,10);
        System.out.println(Arrays.toString(array1));
    }
}
```

## toString method

is used to return a string representation of the array. Which is useful for printing arrays with a single print method without have to use a for loop

### Syntax

`String result = Arrays.toString(array);`

### Example

```Java
import java.util.Arrays;
public class testingTheFillMethod {
    public static void main(String[] args) {
        int[] T = new int[10];

        String result = Arrays.toString(T);
        
        System.out.println(result);
    }
}
```

## Copying methods
### copyOf method

is used to create and return a copy of an array with a specified size

#### Syntax

`datatype array2 = Arrays.copyOf(array1, length);`

- `length` **REQUIRED**: is the size of the copied array.
	- if the length is **smaller** than the original array's length then it will only copy elements up to that length
	- otherwise if the length is **larger** than the original array length then it will copy all elements and it will fill the rest with default values (0 for intergers,,,,etc)

#### Example

```Java
import java.util.Arrays;
public class testingTheCopyOfMethod {
    public static void main(String[] args) {
        int[] array = {5,4,8,9,3,7};

        int[] shorterArray = Arrays.copyOf(array,4);
        System.out.println(Arrays.toString(shorterArray));

        int[] longerArray = Arrays.copyOf(array, 10);
        System.out.println(Arrays.toString(longerArray));
    }
}
```

### copyOfRange method

extremely similar to the [[Temporary/Java/imports/Arrays#copyOf method|copyOf method]] except that you can specify where to start and where to to end copying indexes from the original array

#### Syntax

`datatype array2 = Arrays.copyOfRange(array1, fromIndex, toIndex);`

- just like [[Temporary/Java/imports/Arrays#Sort method|sort method]] you can set the starting index and the ending  index to specify which elements you wan to copy

#### Example

```Java
import java.util.Arrays;
public class testingTheCopyOfMethod {
    public static void main(String[] args) {
        int[] array = {5,4,8,9,3,7};

        int[] shorterArray = Arrays.copyOfRange(array,4,10);
        System.out.println(Arrays.toString(shorterArray));

        int[] longerArray = Arrays.copyOfRange(array, 1,6);
        System.out.println(Arrays.toString(longerArray));
    }
}
```

#### Notes

- if the `toIndex` is **larger** than the size of the original array:
	- the length of the copier array will be **`toIndex - fromIndex`**
		- **Example**: array size = 5 | copyOfRange(array,4,10) --> `10 - 4 = 6` *the length of the copied array will be 6*
	- it will copy elements from the starting index till the end of the original array
	- afterwards it will just fill the rest of the elements with default values

