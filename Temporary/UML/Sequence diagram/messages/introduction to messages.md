messages are arrows pointing from the calling object to the receiver object which contains a method or message (action) to execute

![[image-173.png]]

# Syntax

## for event messages

<h4 style="text-align:center;">SignalOrOperationName(parameters)</h4>

| **Role of the Argument**         | **Syntax**               | **Explanation**                                                                                 | **Example**          |
| -------------------------------- | ------------------------ | ----------------------------------------------------------------------------------------------- | -------------------- |
| **Standard Argument**            | `paramName = paramValue` | Used to assign a specific value to a parameter. not changable                                   | `initialiser(x=100)` |
| **Modifiable Argument (In/Out)** | `paramName : paramValue` | Used to indicate that a parameter (often passed by reference) can be modified by the operation. | `f(x:12)`            |

## for return messages

<h4 style="text-align:center;">targetAttribute = operationName(params):returnValue</h4>

