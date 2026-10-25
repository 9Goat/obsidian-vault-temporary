printf in java is ***almost*** the same as C except for few differences

- for reference for the printf in  C check this note :  [[Printf in C]]

# Differences

## Format Specifiers

- all pointers related specifiers are not included in java
- in java you can display booleans using the `%b` specifier
- in java you cannot use any `%l` specifiers to print long so instead use the `%d`

## precision

unlike C the precision does **NOT** work for integers it works only for strings and floats

## flags

in java instead of the `-` flag there are:

- **`,` comma** : which will separate each 3 digits after the decimal point (if it exists) with a comma
	- **Example**:  10000000.654 ->  10,000,000.654
- **`(`** **close parenthese** : which will surround the number in parenthese **IF** its a negative number
	-  **Example**: -5 -> (5) |   5 -> 5


## return value

unlike C java [[printf]] method  does not return the number of characters that will be printed in the console