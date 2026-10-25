the math class is a **built in** class provided by java to apply basic math in our program here is the list of methods offered by that  class

# Basic math

## abs

Used to get the absolute value of a number (integer, long, float, or double). 

### Syntax

```Java
int intResult = Math.abs(-5); // intResult will be 5
double doubleResult = Math.abs(-10.75); // doubleResult will be 10.75
long longResult = Math.abs(-1234567890123L); // longResult will be 1234567890123L
float floatResult = Math.abs(-3.14f); // floatResult will be 3.14f
```

---

## min

Used to get the smaller of two numbers. It works for `int`, `long`, `float`, and `double`.

### Syntax

```Java
int minInt = Math.min(10, 20); // minInt will be 10
double minDouble = Math.min(5.5, 5.4); // minDouble will be 5.4
```


## max

Used to get the larger of two numbers. It works for `int`, `long`, `float`, and `double`.

### Syntax

```Java
int maxInt = Math.max(10, 20); // maxInt will be 20
double maxDouble = Math.max(5.5, 5.4); // maxDouble will be 5.5
```

## Note

Both [[Math class#min|min]] and [[Math class#max|max]] methods **ONLY** accepts **2** parameters

---

## sqrt

Used to calculate the square root of a `double` value. The result is always a `double`.

### Syntax

```Java
double sqrtResult = Math.sqrt(25.0); // sqrtResult will be 5.0
double sqrtNegative = Math.sqrt(-9.0); // sqrtNegative will be NaN (Not a Number)
```

---

## pow

Used to calculate a number raised to the power of another number (base to the exponent). Both arguments and the result are `double`.

### Syntax

```Java
double powResult1 = Math.pow(2.0, 3.0); // 2 to the power of 3 (2*2*2), powResult1 will be 8.0
double powResult2 = Math.pow(4.0, 0.5); // 4 to the power of 0.5 (square root of 4), powResult2 will be 2.0
```

---

## round

Used to round a `float` or `double` to the nearest `long` or `int` respectively. It uses "round half up" logic (e.g., 2.5 rounds to 3).

### Syntax

```Java
long roundLong = Math.round(3.5); // roundLong will be 4
long roundLong2 = Math.round(3.4); // roundLong2 will be 3
int roundInt = Math.round(3.5f); // roundInt will be 4 (for float input)
```

---

## ceil

Used to round a `double` value **up** to the nearest whole number (or integer). The result is a `double`.

### Syntax

```Java
double ceilResult1 = Math.ceil(7.1); // ceilResult1 will be 8.0
double ceilResult2 = Math.ceil(7.9); // ceilResult2 will be 8.0
double ceilResult3 = Math.ceil(7.0); // ceilResult3 will be 7.0
double ceilResult4 = Math.ceil(-7.1); // ceilResult4 will be -7.0
```

---

## floor

Used to round a `double` value **down** to the nearest whole number (or integer). The result is a `double`.

### Syntax

```Java
double floorResult1 = Math.floor(7.9); // floorResult1 will be 7.0
double floorResult2 = Math.floor(7.1); // floorResult2 will be 7.0
double floorResult3 = Math.floor(7.0); // floorResult3 will be 7.0
double floorResult4 = Math.floor(-7.9); // floorResult4 will be -8.0
```

---

## PI

A `double` constant representing the ratio of the circumference of a circle to its diameter, approximately 3.14159.

### Syntax

```java
double circumference = 2 * Math.PI * radius;
System.out.println("Value of PI: " + Math.PI); // Output: Value of PI: 3.141592653589793
```

---

## E

A `double` constant representing the base of the natural logarithms, approximately 2.71828.

### Syntax

```java
double naturalLogBase = Math.E;
double exponentialResult = Math.pow(Math.E, 2); // e squared
System.out.println("Value of E: " + Math.E); // Output: Value of E: 2.718281828459045
```

