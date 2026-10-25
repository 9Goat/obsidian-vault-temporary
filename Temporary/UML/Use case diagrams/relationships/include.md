include is used as a relation between 2 use cases that share a common functionality to state that a use case **REQUIRES** an another use case to function properly.

# How to create it

include is a dashed line that goes from the use case that includes the functionality of another use case to the included use case, with the word **`<<include>>`** above the line and an open arrowhead pointing to the included use case

![[image-23.png]]
# Example

In a banking system, the main action of **Transfer Funds** always requires the steps involved in **Verify Credentials**.

- **Base Use Case (Invoker):** Transfer Funds
- **Included Use Case (Required):** Verify Credentials

The relationship is read as: **"Transfer Funds always includes Verify Credentials."**

![[image-24.png]]

