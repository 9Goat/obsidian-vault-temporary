
## Basic Information & Length

### length()

Used to get the number of characters in a string.

#### Syntax

```Java
int length = myString.length();
```

#### Example

```Java
public class StringLengthExample {
    public static void main(String[] args) {
        String myString = "Hello Java";
        int length = myString.length();
        System.out.println("The string is: \"" + myString + "\"");
        System.out.println("Length of the string: " + length); // Output: Length of the string: 10
    }
}
```

---

### isEmpty()

Used to check if a string is empty (i.e., has a length of 0).

#### Syntax

```Java
boolean isEmpty = myString.isEmpty();
```

#### Example

```Java
public class StringIsEmptyExample {
    public static void main(String[] args) {
        String emptyString = "";
        String nonEmptyString = "abc";

        boolean isEmpty1 = emptyString.isEmpty();
        boolean isEmpty2 = nonEmptyString.isEmpty();

        System.out.println("Is \"" + emptyString + "\" empty? " + isEmpty1); // Output: Is "" empty? true
        System.out.println("Is \"" + nonEmptyString + "\" empty? " + isEmpty2); // Output: Is "abc" empty? false
    }
}
```

---

## Character Access

### charAt()

Used to get the character at a specified index within the string. Indices are 0-based.

#### Syntax

```Java
char character = myString.charAt(index);
```

#### Example

```Java
public class StringCharAtExample {
    public static void main(String[] args) {
        String myString = "Java";
        char firstChar = myString.charAt(0);
        char lastChar = myString.charAt(3);

        System.out.println("The string is: \"" + myString + "\"");
        System.out.println("Character at index 0: " + firstChar); // Output: Character at index 0: J
        System.out.println("Character at index 3: " + lastChar); // Output: Character at index 3: a

        // Uncommenting the line below would throw an IndexOutOfBoundsException
        // char outOfBounds = myString.charAt(4);
    }
}
```

---

### codePointAt()

Used to get the Unicode code point of the character at a specified index. This is useful for handling characters outside the Basic Multilingual Plane (BMP), such as emojis.

#### Syntax

```Java
int codePoint = myString.codePointAt(index);
```

#### Example

```Java
public class StringCodePointAtExample {
    public static void main(String[] args) {
        String myString = "Hello \uD83D\uDE00"; // "Hello 😀" (😀 is a surrogate pair)
        int codePoint1 = myString.codePointAt(0);
        int codePoint2 = myString.codePointAt(6); // Index of the start of the emoji

        System.out.println("The string is: \"" + myString + "\"");
        System.out.println("Code point of 'H' (index 0): " + codePoint1); // Output: Code point of 'H' (index 0): 72
        System.out.println("Code point of '😀' (index 6): " + codePoint2); // Output: Code point of '😀' (index 6): 128512
    }
}
```

---

## Comparing Strings

### equals()

Used to compare two strings for equality. It returns `true` if the strings are identical (same characters in the same order, case-sensitive), `false` otherwise.

#### Syntax

```Java
boolean isEqual = str1.equals(str2);
```

#### Example

```Java
public class StringEqualsExample {
    public static void main(String[] args) {
        String str1 = "Hello";
        String str2 = "Hello";
        String str3 = "hello";

        boolean isEqual1 = str1.equals(str2);
        boolean isEqual2 = str1.equals(str3);

        System.out.println("\"" + str1 + "\" equals \"" + str2 + "\"? " + isEqual1); // Output: "Hello" equals "Hello"? true
        System.out.println("\"" + str1 + "\" equals \"" + str3 + "\"? " + isEqual2); // Output: "Hello" equals "hello"? false
    }
}
```

---

### equalsIgnoreCase()

Used to compare two strings for equality, ignoring case differences.

#### Syntax

```Java
boolean isEqual = str1.equalsIgnoreCase(str2);
```

#### Example

```Java
public class StringEqualsIgnoreCaseExample {
    public static void main(String[] args) {
        String str1 = "Hello";
        String str2 = "hello";
        String str3 = "World";

        boolean isEqual = str1.equalsIgnoreCase(str2);
        boolean isNotEqual = str1.equalsIgnoreCase(str3);

        System.out.println("\"" + str1 + "\" equalsIgnoreCase \"" + str2 + "\"? " + isEqual); // Output: "Hello" equalsIgnoreCase "hello"? true
        System.out.println("\"" + str1 + "\" equalsIgnoreCase \"" + str3 + "\"? " + isNotEqual); // Output: "Hello" equalsIgnoreCase "World"? false
    }
}
```

---

### regionMatches()

Used to test if two string regions are equal. It has several overloads, allowing for case-sensitivity and specifying start indices and lengths.

#### Syntax

```Java
boolean match = str1.regionMatches(thisOffset, otherString, otherOffset, len);
boolean matchIgnoreCase = str1.regionMatches(true, thisOffset, otherString, otherOffset, len);
```

#### Example

```Java
public class StringRegionMatchesExample {
    public static void main(String[] args) {
        String str1 = "Hello World";
        String str2 = "world";

        // Case-sensitive comparison:
        // (thisOffset, otherString, otherOffset, len)
        boolean match1 = str1.regionMatches(6, str2, 0, 5);
        System.out.println("Case-sensitive match of \"World\" in \"" + str1 + "\" with \"" + str2 + "\": " + match1); // Output: false ('W' vs 'w')

        // Case-insensitive comparison:
        // (ignoreCase, thisOffset, otherString, otherOffset, len)
        boolean match2 = str1.regionMatches(true, 6, str2, 0, 5);
        System.out.println("Case-insensitive match of \"World\" in \"" + str1 + "\" with \"" + str2 + "\": " + match2); // Output: true
    }
}
```

---

## Searching & Checking Content

### startsWith()

Used to check if a string begins with a specified prefix.

#### Syntax

```Java
boolean startsWith = myString.startsWith(prefix);
```

#### Example

```Java
public class StringStartsWithExample {
    public static void main(String[] args) {
        String myString = "Programming";
        boolean startsWithPro = myString.startsWith("Pro");
        boolean startsWithGram = myString.startsWith("Gram");

        System.out.println("The string is: \"" + myString + "\"");
        System.out.println("Starts with \"Pro\"? " + startsWithPro); // Output: Starts with "Pro"? true
        System.out.println("Starts with \"Gram\"? " + startsWithGram); // Output: Starts with "Gram"? false
    }
}
```

---

### endsWith()

Used to check if a string ends with a specified suffix.

#### Syntax

```Java
boolean endsWith = myString.endsWith(suffix);
```

#### Example

```Java
public class StringEndsWithExample {
    public static void main(String[] args) {
        String myString = "Programming";
        boolean endsWithIng = myString.endsWith("ing");
        boolean endsWithGram = myString.endsWith("Gram");

        System.out.println("The string is: \"" + myString + "\"");
        System.out.println("Ends with \"ing\"? " + endsWithIng); // Output: Ends with "ing"? true
        System.out.println("Ends with \"Gram\"? " + endsWithGram); // Output: Ends with "Gram"? false
    }
}
```

---

### contains()

Used to check if a string contains a specified sequence of characters.

#### Syntax

```Java
boolean contains = myString.contains(sequence);
```

#### Example

```Java
public class StringContainsExample {
    public static void main(String[] args) {
        String myString = "Java Programming";
        boolean containsJava = myString.contains("Java");
        boolean containsPython = myString.contains("Python");

        System.out.println("The string is: \"" + myString + "\"");
        System.out.println("Contains \"Java\"? " + containsJava); // Output: Contains "Java"? true
        System.out.println("Contains \"Python\"? " + containsPython); // Output: Contains "Python"? false
    }
}
```

---

### indexOf()

Used to find the index of the first occurrence of a specified character or substring. Returns -1 if not found.

#### Syntax

```Java
int index = myString.indexOf(charOrString);
int indexFrom = myString.indexOf(charOrString, fromIndex);
```

#### Example

```Java
public class StringIndexOfExample {
    public static void main(String[] args) {
        String myString = "hello world hello";
        int index1 = myString.indexOf('o');
        int index2 = myString.indexOf("world");
        int index3 = myString.indexOf('z');
        int index4 = myString.indexOf('o', 5); // Find 'o' starting from index 5

        System.out.println("The string is: \"" + myString + "\"");
        System.out.println("First 'o' at index: " + index1); // Output: First 'o' at index: 4
        System.out.println("First \"world\" at index: " + index2); // Output: First "world" at index: 6
        System.out.println("First 'z' at index: " + index3); // Output: First 'z' at index: -1
        System.out.println("First 'o' from index 5: " + index4); // Output: First 'o' from index 5: 7
    }
}
```

---

### lastIndexOf()

Used to find the index of the last occurrence of a specified character or substring. Returns -1 if not found.

#### Syntax

```Java
int lastIndex = myString.lastIndexOf(charOrString);
int lastIndexFrom = myString.lastIndexOf(charOrString, fromIndex);
```

#### Example

```Java
public class StringLastIndexOfExample {
    public static void main(String[] args) {
        String myString = "hello world hello";
        int lastIndex1 = myString.lastIndexOf('o');
        int lastIndex2 = myString.lastIndexOf("hello");
        int lastIndex3 = myString.lastIndexOf('z');

        System.out.println("The string is: \"" + myString + "\"");
        System.out.println("Last 'o' at index: " + lastIndex1); // Output: Last 'o' at index: 13
        System.out.println("Last \"hello\" at index: " + lastIndex2); // Output: Last "hello" at index: 12
        System.out.println("Last 'z' at index: " + lastIndex3); // Output: Last 'z' at index: -1
    }
}
```

---

### matches()

Used to tell whether or not this string matches the given regular expression.

#### Syntax

```Java
boolean matches = myString.matches(regex);
```

#### Example

```Java
public class StringMatchesExample {
    public static void main(String[] args) {
        String phoneNumber = "123-456-7890";
        boolean isValidPhone = phoneNumber.matches("\\d{3}-\\d{3}-\\d{4}");

        String email = "test@example.com";
        boolean isValidEmail = email.matches("[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\\.[a-zA-Z]{2,}");

        System.out.println("Phone number \"" + phoneNumber + "\" matches regex? " + isValidPhone); // Output: true
        System.out.println("Email \"" + email + "\" matches regex? " + isValidEmail); // Output: true

        String invalidPhone = "12345";
        System.out.println("Phone number \"" + invalidPhone + "\" matches regex? " + invalidPhone.matches("\\d{3}-\\d{3}-\\d{4}")); // Output: false
    }
}
```

---

## Modifying & Transforming Strings

### concat()

Used to concatenate (join) two strings. It returns a new string that is the result of appending the argument string to the end of this string.

#### Syntax

```Java
String result = str1.concat(str2);
```

#### Example

```Java
public class StringConcatExample {
    public static void main(String[] args) {
        String str1 = "Hello";
        String str2 = " World";
        String result = str1.concat(str2);

        System.out.println("String 1: \"" + str1 + "\"");
        System.out.println("String 2: \"" + str2 + "\"");
        System.out.println("Concatenated string: \"" + result + "\""); // Output: Concatenated string: "Hello World"

        // Note: The '+' operator is often preferred for concatenation:
        String plusOperatorResult = str1 + str2 + "!";
        System.out.println("Using '+' operator: \"" + plusOperatorResult + "\""); // Output: Using '+' operator: "Hello World!"
    }
}
```

---

### replace()

Used to replace all occurrences of a specified character or character sequence with another.

#### Syntax

```Java
String newString = myString.replace(oldChar, newChar);
String newString = myString.replace(oldSequence, newSequence);
```

#### Example

```Java
public class StringReplaceExample {
    public static void main(String[] args) {
        String myString = "banana";
        String replacedChar = myString.replace('a', 'o');
        String replacedSeq = myString.replace("an", "AN");

        System.out.println("Original string: \"" + myString + "\"");
        System.out.println("Replaced 'a' with 'o': \"" + replacedChar + "\""); // Output: Replaced 'a' with 'o': "bonono"
        System.out.println("Replaced \"an\" with \"AN\": \"" + replacedSeq + "\""); // Output: Replaced "an" with "AN": "bANANA"
    }
}
```

---

### replaceAll()

Used to replace each substring of this string that matches the given regular expression with the given replacement.

#### Syntax

```Java
String newString = myString.replaceAll(regex, replacement);
```

#### Example

```Java
public class StringReplaceAllExample {
    public static void main(String[] args) {
        String myString = "apple, banana, cherry";
        // Replace all commas and spaces with a single space
        String replacedAll = myString.replaceAll("[, ]+", " ");

        String numbers = "1a2b3c";
        String replacedDigits = numbers.replaceAll("\\d", "_"); // \\d is regex for digit

        System.out.println("Original string: \"" + myString + "\"");
        System.out.println("Replaced all separators: \"" + replacedAll + "\""); // Output: Replaced all separators: "apple banana cherry"
        System.out.println("Original string: \"" + numbers + "\"");
        System.out.println("Replaced all digits: \"" + replacedDigits + "\""); // Output: Replaced all digits: "_a_b_c"
    }
}
```

---

### replaceFirst()

Used to replace the first substring of this string that matches the given regular expression with the given replacement.

#### Syntax

```Java
String newString = myString.replaceFirst(regex, replacement);
```

#### Example

```Java
public class StringReplaceFirstExample {
    public static void main(String[] args) {
        String myString = "apple, banana, cherry";
        // Replace only the first comma and space
        String replacedFirst = myString.replaceFirst("[, ]+", " ");

        String numbers = "1a2b3c";
        String replacedFirstDigit = numbers.replaceFirst("\\d", "_");

        System.out.println("Original string: \"" + myString + "\"");
        System.out.println("Replaced first separator: \"" + replacedFirst + "\""); // Output: Replaced first separator: "apple banana, cherry"
        System.out.println("Original string: \"" + numbers + "\"");
        System.out.println("Replaced first digit: \"" + replacedFirstDigit + "\""); // Output: Replaced first digit: "_a2b3c"
    }
}
```

---

### toLowerCase()

Used to convert all characters in the string to lowercase.

#### Syntax

```Java
String lowerCaseString = myString.toLowerCase();
```

#### Example

```Java
public class StringToLowerCaseExample {
    public static void main(String[] args) {
        String myString = "Hello World";
        String lowerCase = myString.toLowerCase();

        System.out.println("Original string: \"" + myString + "\"");
        System.out.println("Lowercase string: \"" + lowerCase + "\""); // Output: Lowercase string: "hello world"
    }
}
```

---

### toUpperCase()

Used to convert all characters in the string to uppercase.

#### Syntax

```Java
String upperCaseString = myString.toUpperCase();
```

#### Example

```Java
public class StringToUpperCaseExample {
    public static void main(String[] args) {
        String myString = "Hello World";
        String upperCase = myString.toUpperCase();

        System.out.println("Original string: \"" + myString + "\"");
        System.out.println("Uppercase string: \"" + upperCase + "\""); // Output: Uppercase string: "HELLO WORLD"
    }
}
```

---

### trim()

Used to remove leading and trailing whitespace from the string.

#### Syntax

```Java
String trimmedString = myString.trim();
```

#### Example

```Java
public class StringTrimExample {
    public static void main(String[] args) {
        String myString = "   Hello World   ";
        String trimmedString = myString.trim();
        String noChange = "NoTrimNeeded".trim();

        System.out.println("Original string: \"" + myString + "\"");
        System.out.println("Trimmed string: \"" + trimmedString + "\""); // Output: Trimmed string: "Hello World"
        System.out.println("String with no change: \"" + noChange + "\""); // Output: String with no change: "NoTrimNeeded"
    }
}
```

---

## Splitting & Joining Strings

### split()

Used to split a string into an array of substrings based on a delimiter (which is a regular expression).

#### Syntax

```Java
String[] substrings = myString.split(delimiterRegex);
String[] substringsWithLimit = myString.split(delimiterRegex, limit);
```

#### Example

```Java
import java.util.Arrays;

public class StringSplitExample {
    public static void main(String[] args) {
        String csvData = "apple,banana,cherry";
        String[] fruits = csvData.split(",");

        String sentence = "Java is fun";
        String[] words = sentence.split(" ");

        System.out.println("CSV Data: \"" + csvData + "\"");
        System.out.println("Fruits array: " + Arrays.toString(fruits)); // Output: Fruits array: [apple, banana, cherry]

        System.out.println("Sentence: \"" + sentence + "\"");
        System.out.println("Words array: " + Arrays.toString(words)); // Output: Words array: [Java, is, fun]

        String dataWithEmpty = "one,,two,three";
        String[] parts = dataWithEmpty.split(",");
        System.out.println("Parts with empty: " + Arrays.toString(parts)); // Output: Parts with empty: [one, , two, three]
    }
}
```

---

### join()

A **static** method of the `String` class used to join an array of strings or an `Iterable` of strings with a specified delimiter.

#### Syntax

```Java
String joinedString = String.join(delimiter, elements);
```

#### Example

```Java
import java.util.Arrays;
import java.util.List;

public class StringJoinExample {
    public static void main(String[] args) {
        String[] words = {"Hello", "World", "Java"};
        String joinedString = String.join("-", words);

        List<String> items = Arrays.asList("one", "two", "three");
        String joinedList = String.join(", ", items);

        System.out.println("Words array: " + Arrays.toString(words));
        System.out.println("Joined with '-': \"" + joinedString + "\""); // Output: Joined with '-': "Hello-World-Java"

        System.out.println("Items list: " + items);
        System.out.println("Joined with ', ': \"" + joinedList + "\""); // Output: Joined with ', ': "one, two, three"
    }
}
```

---

## Formatting Strings

### format()

A **static** method of the `String` class used to return a formatted string using the specified format string and arguments. Similar to `printf` in C.

#### Syntax

```Java
String formattedString = String.format(formatString, args...);
```

#### Example

```Java
public class StringFormatExample {
    public static void main(String[] args) {
        String name = "Alice";
        int age = 30;
        double height = 1.75;
        String formattedString = String.format("Name: %s, Age: %d, Height: %.2f meters", name, age, height);

        System.out.println("Formatted string: \"" + formattedString + "\"");
        // Output: Formatted string: "Name: Alice, Age: 30, Height: 1.75 meters"

        String price = String.format("Price: $%.2f", 19.995);
        System.out.println(price); // Output: Price: $20.00
    }
}
```

---

## Substrings

### substring()

A substring method used to get a smaller string that is inside another string.

#### Syntax

```Java
String result = name.substring(start);
String result = name.substring(start, end);
```

-   **start (REQUIRED)**: `int` value that indicates where to start collecting the substring.
    *   The start value is **inclusive**, meaning that the character at this position will be included in the substring.
-   **end (OPTIONAL)**: `int` value that indicates where to stop collecting the substring.
    *   The end value is **exclusive**, meaning that the character at this position will **NOT** be included. To include it, you would use `end + 1`.
-   **NOTE**: If the `end` value is not provided, the substring will extend to the end of the original string (including the final character).

#### Example

```Java
public class SubstringExample {
    public static void main(String[] args) {
        String text = "Hello, World!";

        // Substring from index 0 up to (but not including) index 5
        String substring1 = text.substring(0, 5);
        System.out.println("Substring (0, 5): \"" + substring1 + "\""); // Output: Substring (0, 5): "Hello"

        // Substring from index 7 to the end of the string
        String substring2 = text.substring(7);
        System.out.println("Substring (7): \"" + substring2 + "\""); // Output: Substring (7): "World!"

        // Substring from index 7 up to (but not including) index 12
        String substring3 = text.substring(7, 12);
        System.out.println("Substring (7, 12): \"" + substring3 + "\""); // Output: Substring (7, 12): "World"
    }
}
```

