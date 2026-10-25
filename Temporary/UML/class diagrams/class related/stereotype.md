stereotype is used to explain the state of the class and what it represents.We can either follow a set of defined stereotypes or we can create our own stereotypes.

![[image-51.png]]
# Syntax

```
«stereotypeName»  ClassName
```

- **Placement:** The stereotype name is enclosed in **guillemets** (double-angle brackets: `« »`).
- **Location:** It is placed **above** the class name in the top compartment of the UML class rectangle.

# types of stereotypes

### 1. **`«enumeration»` (Enumération)**

- **Purpose:** Used to model a type whose value is restricted to a fixed, named set of constants (e.g., traffic light colors: `RED`, `YELLOW`, `GREEN`).

### 2. **`«utility»` (Utilitaire)**

- **Purpose:** Used to model classes that contain only **static** attributes and operations (methods) and are never meant to have instances (objects) created from them (e.g., a `MathHelper` class).

### 3. **`«actor»` (Acteur)**

- **Purpose:** Used to represent the external entities (humans or systems) that interact with the system being modeled, often bridging from a Use Case Diagram to a Class Diagram.

### 4. **`«interface»` (Interface)**

used to explain that the class is used as an [[interfaces]]

### 5. **`«exception»` (Exception)**

- **Purpose:** Used to explicitly model classes intended to be thrown or caught as errors during program execution (e.g., `FileNotFoundException`).