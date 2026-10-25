# association title name

the name of the association must be something that can represent all the classes in the association and it must be a verb + an optional adjective:

- verbale active (“travaille pour”) 
- passive (“employé par”).

they are placed above the association line in the middle.we could *OPTIONALY* add an arrow to showcase the direction of the association title

## Example

![[image-57.png]]

# roles

**association roles** are essentially used as a replacement for a general association title *OPTIONALY* (the name placed over the line) to provide a more specific and contextual description of the relationship.

A role indicates **how one class views the other**.

- Instead of simply labeling a connection between `Company` and `Person` as "works for," roles specify the relationship from both sides:
    
    - The **Company's** view of the **Person** is that of an **`employee`**.
    - The **Person's** view of the **Company** is that of an **`employer`**.

association roles directly reflect the **attributes** that will be created in the classes when the model is translated into code.

example java code of roles:

| **Class (Source)** | **Role Name (Pseudo-Attribute)** | **Destination Class (Type)** | **Code Implication**                               |
| ------------------ | -------------------------------- | ---------------------------- | -------------------------------------------------- |
| `Company`          | `employee`                       | `Person`                     | `class Company { private List<Person> employee; }` |
| `Person`           | `employer`                       | `Company`                    | `class Person { private Company employer; }`       |

we are **NOT** required to write the role for all classes we can instead just write it to one of them which is especially useful if we have multiple association towards the same class

## Example 1

![[image-58.png]]

## Example 2

![[image-56.png]]