# Methods

a method in essentially a function inside a class

## Syntax

```Java
class className{

returnDatatype methodName(parameters){
//code here
//return if needed
}

}
```

## Notes

- methods can **ONLY** be created at the **TOP** level class meaning we cannot create a method inside a method
# Objects

an object is an instance of a class meaning when we call a class to access its variables and methods we access it via an object

## Syntax

`className variable = new className()`

## Accessing via objects

by using objects we can access any variable or method declared within the class we creating an instance of

### Accessing variables

to do that we have to call the variable name of the object dot the variable name inside the class here is an example

#### Example

```Java
public class test {

public static void main(String[] a){

student newStudent = new student();
newStudent.grades = 10;

System.out.println(newStudent.grades);

}
}

class student {
int grades;
}
```

### Accessing methods

is the same thing as [[Methods & Objects#Accessing variables|accessing variables]] except that we add parentheses after the name of the method we want to call

#### Example

```Java
public class test {

public static void main(String[] a){

resultCalculator calculator = new resultCalculator();
int average = calculator.calculate(10, 20);
System.out.println(average);

}
}

class resultCalculator{

int calculate(int grades1, int grades2){
return (grades1 + grades2) / 2;
}
```


# Example of using objects and methods

```Java
public class testingClassesAndObjects {
public static void main(String[] args) {

// Creating a new Car object

Car myCar = new Car();

myCar.make = "Ford";
myCar.model = "Mustang";
myCar.year = 2022;

myCar.startEngine();
}
}

class Car {

String make;
String model;
int year;

public void startEngine() {
System.out.println("The engine is starting.");
}
}
```

