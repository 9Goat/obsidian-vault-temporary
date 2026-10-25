
# Syntax

```
visibility [/] attributeName : type [{constraint}] [= defaultValue]
```

- [] means **OPTIONAL**
## 1. Visibility (`<visibilite>`) 

This defines the access level, corresponding to programming language access modifiers.

- `+`: **public** (Visible everywhere)
- `#`: **protected** (Visible within the class and its subclasses)
- `-`: **private** (Visible only within the defining class)
- `~`: **package** (Visible only within the same package/namespace)

## 2. Derived Indicator (`/`)

- `/`: Signals a **derived attribute**. This means the attribute's value is **calculated** (or computed) from other attributes/methods, rather than being stored directly.

## 3. Attribute Name (`nomAttribut`) 

- The name used to identify the attribute. It's typically written in **camelCase** (e.g., `accountBalance`).

## 4. Type (`type`) 

- The data type of the attribute (e.g., `String`, `Integer`, `Date`, or the name of another class).
## 5. Constraint (`{<contrainte>}`)

- Used to specify **OCL (Object Constraint Language) constraints** or general properties when the multiplicity is greater than one (though constraints can apply generally). Common properties include:
- `{readOnly}`: The attribute cannot be modified after initialization.
- `{unique}`: All values in a multi-valued attribute must be unique.
- `{ordered}`: The values in a multi-valued attribute maintain a specific order.

## 6. Default Value (`<valeurParDefaut>`)

- The initial value assigned to the attribute when an instance of the class is created.

# Example

1. **Public, simple attribute:**  
    `+ customerName : String`  
2. **Private, with default value:**  
    `- balance : Double = 0.0`  
3. **Protected, derived attribute:**  
    `# /fullName : String`  
4. **Package-level, read-only attribute:**  
    `~ creationDate : Date {readOnly}`  
5. **Private, with a specific constraint and default:**  
    `- age : Integer {age > 0} = 18`  

