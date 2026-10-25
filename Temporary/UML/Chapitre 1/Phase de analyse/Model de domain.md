the Analysis phase starts to look **inside** to describe the business problem in a language.

# Key Characteristics:

- **Static View:** It represents the structure of the information, not how it moves.
- **Business Concepts (Entities):** It defines the "things" the system handles. In your library system, these are entities like **Livre** (Book), **Auteur** (Author), and **Client**.
- **Attributes Only:** These classes describe the properties of the entities. For a "Livre," attributes include the **title, ISBN, and price**.
- **No Operations:** A crucial rule is that Domain Model classes **must not contain operations** (methods/functions). We only care about the data at this stage, not the behavior.
- **Associations:** It shows how these entities are linked. For example, a **Livre** "is written by" an **Auteur**.

**BASICALLY IS CLASS DIAGRAM BUT SIMPLIFIED AND WITHOUT METHODS/OPERATIONS**

# Example

![[image-313.png]]

