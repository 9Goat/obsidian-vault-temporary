in object diagram we label instances/objects with the following syntax

<h4 style="text-align:center;text-decoration:underline;">ObjectName : Class name</h4>

inside a rectangle and underlined like this

![[image-139.png]]

# 1. Named specific labels

- **Syntax:** `objectName : ClassName`
- **Definition:** The object is given a unique, specific name (`objectName`) within the context of the diagram. This name refers to a single, real-world instance or a specific variable in the code.
- **Example:** If you have a `Customer` class, you might name a specific instance `john_doe`.

<h4 style="text-align:center;text-decoration:underline;">john_doe : Customer​</h4>

# 2. Anonymous Object (Instance without a Name)

This is what you referred to as an "anonymous" object.

- **Syntax:** `: ClassName` (The object name space is left blank).
- **Definition:** The object belongs to the specified class, but its specific instance name is unimportant or irrelevant to the scenario being modeled. It represents _any_ instance of that class.
- **Example:**

<h4 style="text-align:center;text-decoration:underline;">: Order​</h4>

# 3. Stereotyped Object

This method uses the concept of **stereotypes** to categorize the object's role,it follows the same sterotypes from [[stereotype]]  class diagrams
- **Syntax:** `objectName : ClassName <<stereotype>>`
- **Definition:** A stereotype is a way of extending the UML notation to indicate a special usage or role.
- **Example:**

![[image-140.png]]


# 4. State Notation (The Active State Label)

To emphasize the current, active state without always listing the attribute name, UML allows the state to be placed **after the object's name and before the attribute list**, usually within **square brackets** `[ ]`.

- **Syntax:** objectName : ClassName​[current state]
- **Example**:if we want to state that the robot is  in moving state
![[image-141.png]]

# Note

we can combine all of those types and form labels  however we want

