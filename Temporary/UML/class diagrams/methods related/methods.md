# Syntax

```
visibility operationName ([param1, ..., paramN]) : returnType  [ { properties } ]
```

## 1. Visibility (`<visibilite>`)

This defines the access level of the operation, corresponding to programming language access modifiers.

- `+`: **public** (Visible everywhere)
- `#`: **protected** (Visible within the class and its subclasses)
- `-`: **private** (Visible only within the defining class)
- `~`: **package** (Less common; visible only within the same package/namespace)

## 2. Operation Name (`nomOperataion`)

- The name of the method (typically written in **camelCase** for programming languages like Java/C#).
    

## 3. Parameters (`<param1>, ..., <paramN>`)

- A comma-separated list of the operation's parameters, enclosed in parentheses `()`.
- Each parameter must follow its own syntax, which is typically: `[direction] name : type [= defaultValue] {propertyString}`.
    - **Example:** `(id : Integer, count : Integer = 1)`


## 4. Return Type (`<typeRetour>`)

- A colon (`:`) followed by the data type of the value returned by the operation (e.g., `String`, `Boolean`, `void`). If the operation returns no value (like a `void` method), the return type can be omitted.
    

## 5. Properties (`{<proprietes>}`)

- Constraints, indications, or keywords enclosed in curly braces (`{}`) that specify details about the operation. Common properties include:
    
    - `{abstract}`: Indicates the operation has no implementation and must be overridden by subclasses. The operation name is also typically shown in **italics**.
    - `{static}`: Indicates the operation belongs to the class itself, not an instance. The entire operation line is **underlined**.
    - `{query}`: Indicates the operation queries the system state but does not modify it.

# Example

Based on the syntax and explanations in your note [[methods]], here are a few examples of methods:

1.  **Public method with no parameters and no return type:**
    `+ activateAccount(): void`
2.  **Private method with parameters and a return type:**
    `- calculateDiscount(price : Double, percentage : Double) : Double`
3.  **Protected, static method with a default parameter value:**
    `# generateId(prefix : String) : String`
4.  **Public, abstract method:**
    `+ processPayment(amount : Double): void {abstract}`
5.  **Public method with multiple parameters and properties:**
    `+ updateProfile(name : String, email : String, phone : String) : Boolean 
