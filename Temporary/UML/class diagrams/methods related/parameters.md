# Syntax

```
[direction] parameterName : type [ = defaultValue ]
```

## 1. Direction (`[<direction>]`)

The direction specifies how the parameter is used and how its value might change during the operation.

| Value       | Meaning in English  | Description                                                                                                                                                                         |
| ----------- | ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`in`**    | **Input** (Default) | The caller provides a value, but the operation **cannot change** the original value passed. It's a read-only parameter within the operation's scope.                                |
| **`out`**   | **Output**          | The parameter is used only for output. The caller **does not provide** an initial value, and the operation's final result is available to the caller through this parameter.        |
| **`inout`** | **Input/Output**    | The caller provides an initial value, and the operation is **permitted to modify** that value. The final modified value is available to the caller upon the operation's completion. |

## 2. Parameter Name (`<nom_paramètre>`)

- The name of the parameter used within the operation's logic (e.g., `amount`, `customerID`).

## 3. Type (`<type>`)

- A colon (`:`) followed by the data type of the parameter (e.g., `Integer`, `String`, `Address`).

## 4. Default Value (`[=<valeur_par_défaut>]`)

- An equals sign = followed by the value the parameter will take if the caller does not explicitly supply one

# Example


1.  **Basic Input Parameters (default `in`)**:
    `+ calculateArea(length: Double, width: Double): Double`
2.  **Input/Output Parameter (`inout`)**:
    `+ processTransaction(inout balance: Double, amount: Double)`
3.  **Output Parameter (`out`)**:
    `+ fetchData(query: String, out result: String)`
4.  **Parameter with Default Value**:
    `+ logMessage(message: String, level: String = "INFO")`
5.  **Combined Example**:
    `+ configureDevice(inout settings: Map, out status: Integer, timeout: Integer = 60)`