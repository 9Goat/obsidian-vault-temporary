setters and getters are methods that are used to either return or modify the value of a [[access modifiers#Private|Private instance variable]] 

# Getter Methods (Accessors)

A getter method is used to retrieve (get) the value of a private instance variable.

- **Naming Convention**: Getters typically start with `get` followed by the name of the variable (e.g., `getName()`, `getAge()`). For boolean variables, they often start with `is` (e.g., `isActive()`).
- **Return Type**: The return type of a getter method matches the data type of the instance variable it is retrieving.
- **Parameters**: Getters usually do not take any parameters.

# Setter Methods (modifiers)

A setter method is used to modify (set) the value of a private instance variable.

- **Naming Convention**: Setters typically start with `set` followed by the name of the variable (e.g., `setName()`, `setAge()`).
- **Return Type**: Setters usually have a `void` return type, as their primary purpose is to modify a state, not return a value.
- **Parameters**: Setters take one parameter, which is the new value to be assigned to the instance variable. The parameter's data type should match the instance variable's data type.

# Example

```Java
class Product {
    private String itemName; // Private instance variable

    // Getter method
    public String getItemName() {
        return itemName;
    }

    // Setter method
    public void setItemName(String name) {
        this.itemName = name;
    }
}

public class ProductDemo {
    public static void main(String[] args) {
        Product myProduct = new Product();

        // Use setter to set the value
        myProduct.setItemName("Laptop");
        System.out.println("Item Name set to: " + myProduct.getItemName()); // Output: Item Name set to: Laptop

        // Use setter to change the value
        myProduct.setItemName("Mouse");
        // Use getter to retrieve the updated value
        System.out.println("Item Name updated to: " + myProduct.getItemName()); // Output: Item Name updated to: Mouse
    }
}
```

