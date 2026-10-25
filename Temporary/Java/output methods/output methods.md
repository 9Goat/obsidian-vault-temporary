the System.out offers a way to print output to the console in Java.

# print method

this the standard print method in java, it allows us to print messages to the console **WITHOUT** a line separater at the end

## Syntax

```Java
System.out.print(message or value we want to print);
```

- within the parentheses of the **`print`** method we can either have text or a variable that we want to display on the console.
- to combine multiple text or values, we can use the "+" operator within the print method.
- if we want to add a line separater between each print method we have to add at the end of the message **`\n`**

## Example

```Java
public class PrintMethodExample {

    public static void main(String[] args) {
        String name = "Alice";
        int age = 30;

        System.out.print("Hello, "); // Text
        System.out.print(name);      // Variable
        System.out.print("! You are " + age + " years old.\n"); // Combined text/variables with newline

        System.out.print("This is on a new line.");
    }
}
```

# println method

is the exact same as the print method, but it automatically adds a line separator at the end, so you don't need to include `\n` at the end of the message.

## Syntax

```Java
System.out.println(message or value to be printed);
```

## Example

```Java
public class PrintlnMethodExample {
public static void main(String[] args){

System.out.println("Hello");
System.out.println("World");

}}
```

