is An attribute used on an association line to act like a lookup key, allowing you to instantly select one specific object from a large group.With the help of qualifier we can reduce the * many [[multiplicity]] to a much smaller number like one by passing a single qualifier

Think of a **library** that has thousands of **books**.

- **Unqualified Association:** Asking the library for all its books. (Multiplicity: `*`)
- **Qualified Association:** Asking the library for a book by its **ISBN number** (the qualifier). (Multiplicity: `0..1`)

The **ISBN number** is the qualifier that lets you bypass the large collection and go straight to a single, unique item.

# Examples

![[image-78.png]]
![[image-79.png]]

