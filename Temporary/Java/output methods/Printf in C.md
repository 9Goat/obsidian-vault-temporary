the printf function is used to display **formatted** display in this syntax:

`printf(format_string, argument1, argument2,,,etc);`

# format string

format string is a string inside [[Char character in C#String literals|string literals]] which contains **specifiers** that determine how the arguments will be displayed

## Format Specifiers

Format specifiers are special characters that begin with a '%' sign and determine the type of argument that will be displayed. They also specify the format of the output. Here is a list of common format specifiers in C:


| Format Specifier | Description                                                                                                                                                                   | Example                                                                                                                                         |
| :--------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------- |
| `%d` or `%i`     | Signed decimal integer. Prints an integer in base 10. `%i` also interprets input in octal or hexadecimal if prefixed by `0` or `0x` respectively (only in `scanf`).           | `printf("%d", 123);` Output: `123`<br>`printf("%i", 017);` Output: `15` (octal input)<br>`printf("%i", 0x1A);` Output: `26` (hexadecimal input) |
| `%u`             | Unsigned decimal integer. Prints an integer in base 10, treating it as unsigned (always positive or zero).                                                                    | `printf("%u", 4294967295U);` (assuming 32-bit int) Output: `4294967295`                                                                         |
| `%ld`            | Signed long decimal integer. Prints a `long int` in base 10.                                                                                                                  | `long int big_num = 1234567890L; printf("%ld", big_num);` Output: `1234567890`                                                                  |
| `%o`             | Unsigned octal integer. Prints an integer in base 8 (using digits 0-7).                                                                                                       | `printf("%o", 10);` Output: `12`                                                                                                                |
| `%x` or `%X`     | Unsigned hexadecimal integer. Prints an integer in base 16 (using digits 0-9 and letters a-f or A-F). `%x` uses lowercase letters, and `%X` uses uppercase.                   | `printf("%x", 26);` Output: `1a`<br>`printf("%X", 26);` Output: `1A`                                                                            |
| `%c`             | Character. Prints a single character.                                                                                                                                         | `printf("%c", 'A');` Output: `A`                                                                                                                |
| `%f`             | Floating-point number (decimal notation). Prints a `float` or `double` in decimal notation (e.g., 3.14159).                                                                   | `printf("%f", 3.14159);` Output: `3.141590`                                                                                                     |
| `%lf`            | Double floating-point number. Used in `scanf` to read a `double`. In `printf`, using `%f` is sufficient for both `float` and `double` due to implicit argument promotion.     | `double pi = 3.141592653589793; scanf("%lf", &pi); printf("%lf", pi);`                                                                          |
| `%e` or `%E`     | Floating-point number (scientific notation). Prints a `float` or `double` in scientific notation (e.g., 1.234568e+002). `%e` uses lowercase 'e', and `%E` uses uppercase 'E'. | `printf("%e", 123.45678);` Output: `1.234568e+002`<br>`printf("%E", 123.45678);` Output: `1.234568E+002`                                        |
| `%s`             | [[Strings]]. Prints a sequence of characters until a null terminator (`\0`) is encountered.                                                                                   | `char str[] = "Hello";` `printf("%s", str);` Output: `Hello`                                                                                    |
| `%%`             | Used to print a percentage sign                                                                                                                                               | `printf("%%")` Output:`%`                                                                                                                       |
| `%p`             | Pointer. Prints the memory address pointed to by a pointer variable.  The format of the output depends on the system.                                                         | `int num = 10; int *ptr = &num; printf("%p", ptr);` Output: (e.g., `0x7ffe00001234`)                                                            |
| `%zu`            | Used to print values of type [[sizeof()]], which is an unsigned integer type returned by [[sizeof()]].                                                                        | `size_t size = sizeof(int); printf("Size of int: %zu bytes", size);` Output `Size of int: 4 bytes`                                              |

# Modifiers

Modifiers are use to change the display of a format specifier by adding additional context to it here is the last of them

| Modifier     | Simplified Description                                                                                                                                                                                                                                                                                                                                                         | Example                                                                                                                                                                  |
| :----------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `width`      | Sets the *minimum* number of characters to display. If the value is shorter, it adds spaces from **BEFORE** the number if the width is positive otherwise the spaces will be added **AFTER** if the width is negative                                                                                                                                                          | `printf("%5d", 12);` Output: `   12` (three spaces then 12)<br>`printf("%2d", 1234);` Output: `1234` (no padding because value is longer)                                |
| `.precision` | <ul><li>For numbers with decimals (`%f`, `%e`, `%E`): Sets how many digits are shown *after* the decimal point.</li><li>For whole numbers (`%d`, `%i`, etc.): Sets the *minimum* number of digits to show, adding leading zeros if needed.</li><li>For text (`%s`): Sets the *maximum* number of characters to print.</li></ul>                                                | `printf("%.2f", 3.14159);` Output: `3.14`<br>`printf("%.3d", 5);` Output: `005`<br>`printf("%.3s", "Hello");` Output: `Hel`                                              |
| `flags`      | These add extra formatting options:<ul><li>`-`: Left-aligns the output (normally it's right-aligned).</li><li>`+`: Always shows the sign (`+` or `-`) for numbers.</li><li>`0`: Adds leading zeros instead of spaces (only if a width is also specified).</li><li>`space`: if the number is negative do nothing if its positive add space at the front of the number</li></ul> | `printf("%-5d", 12);` Output: `12   `<br>`printf("%+d", 5);` Output: `+5`<br>`printf("%05d", 12);` Output: `00012`                     `printf(% d",18);` Output:  ` 18` |
## NOTE

- any combination of those flags is possible
- the **`.precision`** for float numbers if the number of how many digits after a decimal point is smaller than the actual number of digits after the decimal points the system will round the  number up before removing them in display
	- **Example**: `printf("%.3f", 3.14159);` Output: `3.142` instead of `3.14`**`1`** because round(1.59) -> **2** 

# Argument

for each [[stdio.h#Format Specifiers|Specifier]] we have in our printf we need an argument to make it display in the same position of that specifier .Here is how it works:

- **equality** for [[stdio.h#printf()|printf()]] the number of arguments **must** match the number of [[stdio.h#Format Specifiers|Specifiers]]
- **order** [[stdio.h#Format Specifiers|Specifiers]] and arguments are read from left-to-right meaning the leftmost argument will be applied to the leftmost specifier and so on ,,,

# Example

```c
#include <stdio.h>

int main() {
int age = 30;
char name[] = "Alice";

printf("Hello, %s! You are %d years old.\n", name, age); // Output: Hello, Alice! You are 30 years old.
return 0;
}
```

# Return

printf does have a return value and that return value is equal to the number of characters successfully got display as output (positive integer)

**Note** in case of a failure the return number will be **-1**

## Example

```c
#include <stdio.h>
int main() { 

int chars_printed; 

chars_printed = printf("Hello, world!\n"); 
printf("printf() returned: %d\n", chars_printed); // Output: printf() returned: 14 (13 chars + \n) 

chars_printed = printf("Number: %d\n", 12345); 
printf("printf() returned: %d\n", chars_printed); // Output: printf() returned: 11 

return 0; }

```

