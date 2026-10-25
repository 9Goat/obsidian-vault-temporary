In java exceptions are errors that occure during the runtime/execution the program,If these signals are not handled, the program's execution is typically terminated(code after the line where the exception occurred is not executed)., leading to an application crash.

exceptions in Java are **true objects**. When an error occurs, the Java runtime environment instantiates an object that contains detailed information about the error, including its type and the state of the program when it happened,.

# What are  throwables?

##  Definition

The `Throwable` class directly inherits from `java.lang.Object`. It provides the fundamental mechanism for capturing the state of the program at the exact moment an exception occurs.

To be considered an exception, an object must be an instance of a class that inherits from the **java.lang.Throwable** class.

## Throwables hierarchy

![[image-262.png]]

The exception class provides 3 methods that can help us understand the exception which are:

| **Method**              | **Returns** | **Description**                                               |
| ----------------------- | ----------- | ------------------------------------------------------------- |
| **`getMessage()`**      | `String`    | Returns only the error message (the "why").                   |
| **`toString()`**        | `String`    | Returns the class name + the message.                         |
| **`printStackTrace()`** | `void`      | Prints the full history of the error (the "where" and "how"). |
## Checked vs Unchecked exceptions

in Java there are 2 types  of  exceptions which are checked and unchecked Exceptions.

- **Checked Exceptions** are for "Bad things that _might_ happen" even if your code is perfect (like a server being down or a file being missing). The compiler forces you to have a backup plan (a `catch` block). 
- **Unchecked Exceptions** are for "Things that _shouldn't_ happen" if the code is written correctly.

### Checked exceptions

These are subclasses of `Exception` that are **not** subclasses of `RuntimeException`. The compiler **strictly enforces** that you either handle them with `try-catch` or declare them with `throws`.

If it sees a method that might throw a Checked Exception (like `IOException`), it stops you and says: _"I won't turn this into bytecode until you tell me exactly what to do if this fails."_. They are basically exceptions that can be determined before the program is run, such as a file not being found.

- **When:** Before the program starts.
- **Goal:** To ensure the "environmental" risks (missing files, network drops) are handled by the programmer.

#### Example

![[image-263.png]]

when we try to open a file that doesn't exist, Java tells us that we need to handle that exception otherwise it wont compile the program.

### Unchecked exceptions

These represent "bugs" or logic errors that usually occur due to poor programming. Because they can happen anywhere, the compiler does not force you to handle them explicitly.

- **Hierarchy:** Any subclass of `RuntimeException` (which itself inherits from `Exception`).
- **The Rule:** You are not required to catch or declare these. Instead, you should focus on writing better logic to prevent them from happening in the first place.

#### Example

```Java
public class UncheckedExample {
    public static void main(String[] args) {
        int[] scores = {90, 85, 70};
        
        // This will compile, but crash at runtime
        System.out.println(scores[5]); 
    }
}
```
- **Unchecked exceptions are typically programming errors**. Like in this example we are trying to access an array index that doesn't exist, which results in an `ArrayIndexOutOfBoundsException`.
# How to handle exceptions


there are 3 main tools that we use in the handle approach which are the following:

- **try**: to test the code that may contains the error*
- **catch**: to catch a specific error and execute a code depending on the type of that error
- **finally**: to execute a block of code that should always execute no matter if there is an exception or not (useful for things like closing file or scanner)

## Try and catch


If an exception occurs in the `try` block, Java looks for a `catch` block that matches the type of exception thrown.

- **Specific to General:** You can have multiple catch blocks. You must catch the most specific exceptions (like `ArithmeticException`) before general ones (like `Exception`). *Otherwise the compiler wont allow us to execute the code if a general exception is catched before a specific one since it will be considered as unreachable code.*
- **The Parameter:** The `(Exception e)` part is actually a variable declaration. You can use `e.getMessage()` or `e.printStackTrace()` to understand what went wrong.

### Syntax

```java
try {
    // Code that might throw an exception
} catch (ExceptionType1 e) {
//exception 1 statements here
}catch(ExceptionType2 e2){
//exception 2 statements here
}// ,,,etc
```

### Example

```Java
try {
    FileReader fr = new FileReader("exam_notes.txt");
    fr.read();
} 
// 1. Most Specific: Handle just the missing file
catch (FileNotFoundException e) {
    System.out.println("The specific file is missing. Please check the path.");
} 
// 2. More General: Handle any other IO issues (disk error, etc.)
catch (IOException e) {
    System.out.println("A general IO error occurred.");
} 
// 3. Most General: The "Safety Net" for everything else
catch (Exception e) {
    System.out.println("Something else went wrong: " + e.getMessage());
}
//statements here will execute as well
```

### Note

after we catch an exception the program will continue running normally

## Finally(optional)

The `finally` block **always** executes, whether an exception was thrown or not, and even if there was a `return` statement in the `try` or `catch` blocks.

**Why use it?** To close resources. If you open a file or a database connection in the `try` block, you _must_ close it in the `finally` block to prevent memory leaks.

### example

```Java
FileReader reader = null;
try {
    reader = new FileReader("exam_topics.txt");
    // read file...
} catch (IOException e) {
    System.out.println("Could not read file.");
} finally {
    System.out.println("Closing the file reader...");
    if (reader != null) {
        try { reader.close(); } catch (IOException e) { /* ignore */ }
    }
}
```

# Custom exceptions

this section will cover how to create custom exception classes AND more importantly how to use throw and throws (they also work for built in exceptions not just custom):

- **throw**: throw an exception with an optional error message.
- **throws** this is mendatory to declare that a method might throw a checked exception, so that it throws the exception to a try catch block instead of just crashing the program.

## How to create custom exceptions

To create your own exception, you must inherit from `Exception` or any of its subclasses. (for a **Checked** exception) or `RuntimeException` (for an **Unchecked** one).

### Example

```Java
class CheckedException extends Exception {

public CheckedException(String message) { //OPTIONAL: constructor to pass a message to the exception getMessage() method
super(message);
}

public CheckedException() { //OPTIONAL: default constructor
super();
}

}
```

## throw

Used to actually trigger the exception object. The `throw` keyword is utilized when you want to signal that an exceptional condition has occurred.

### Syntax

```Java
try {
throw new CheckedException("this is a checked exception"); //this triggers the exception to be thrown, and the message is passed to the getMessage() method
} catch (CheckedException e) {
e.getMessage();
}
```

### Example

in this example we create a new exception that checks if the user age is is older than 18

```Java
public class test  
{  
public static void main(String[] args) {  
try {  
int age = 15;  
if (age < 18) {  
throw new IllegalAgeException("Age must be at least 18");  
}  
} catch (IllegalAgeException e) {  
System.out.println(e.getMessage());  
}  
}  
}  
class IllegalAgeException extends Exception {  
public IllegalAgeException(String message) {  
super(message);  
}  
}
```

### Note

inside the throw statement  we can provide the exception with either:

- no parameters, which  will basically call the default constructor of the exception.
- a custom message which will be available through the `getMessage()` method of the exception object.
##  throws

in the case we are working with a method that might throw a Checked Exception, we need to either handle it with a try-catch block or declare it with the "throws" keyword. Using the key word throws make the problem ignore the Checked Exception and pass it to the caller method.

### Syntax

```Java
public datatype functionName(parameters) throws exceptionName{
//statement that causes a checked exception
}
```

### Example

in this example we are executing the throw statement inside a method without using try and catch which is why we **MUST** add the throws statement to it otherwise we will get an errors

```Java
public class test  
{  
public static void main(String[] args) {  
try {  
ToTestMethod test = new ToTestMethod();  
test.someMethod();  
} catch (IllegalAgeException e) {  
System.out.println(e.getMessage());  
}  
}  
}  
class IllegalAgeException extends Exception {  
public IllegalAgeException(String message) {  
super(message);  
}  
}  
  
class ToTestMethod{  
public void someMethod() throws IllegalAgeException {  
int age = 15;  
if (age < 18) {  
throw new IllegalAgeException("Age must be at least 18");  
}  
}  
}
```

