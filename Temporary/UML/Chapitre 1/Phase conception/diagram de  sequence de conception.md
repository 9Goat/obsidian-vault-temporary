# 1. What is it?

The Detailed Sequence Diagram shows the chronological interactions between the specific objects we defined in our Design Class Diagram (DCD). It represents a "script" where objects from different classes collaborate to fulfill a specific Use Case.

# 2. The Components

Instead of just one box for the "System," we now see multiple lifelines representing the three types of classes (Jacobson Stereotypes):

- **Actor:** Initiates the action.
- **Boundaries (****«dialogue»****):** Receives the message from the actor.
- **Controls (****«contrôle»****):** Receives the logic request from the boundary.
- **Entities (****«entité»****):** Provides or stores the data requested by the control.

# 3. The "Golden Rule" of Design Consistency

Your course materials highlight a fundamental rule that ensures your diagrams are ready for coding:

**"A message can only be received by an object if its class has declared the corresponding public operation"**.

This means if you draw an arrow called `calculerTotal()` pointing to a `Panier` object in your sequence diagram, that exact method **must** exist as a public operation in the `Panier` class in your Class Diagram. If it’s not in the Class Diagram, the Sequence Diagram is "illegal."

# Examples

**From this class diagram**

![[image-333.png]]

**To this**

![[image-332.png]]