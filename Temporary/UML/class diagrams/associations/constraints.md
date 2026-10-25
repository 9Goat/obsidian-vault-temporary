we can specify constraints on associations by writing them inside of curly brackets **`{}`**

# Types of constraints

## Subset

to be a part of this association must also have an instance in the other association (which is very similar to include in database design) 

### Example

![[image-66.png]]
![[image-67.png]]

## XOR

The `{XOR}` means that class `A` must have either an association to `B` or to `C` but not to both or none.

### Example

![[image-68.png]]

## frozen & addonly

The `{frozen}` constraint (often called **`{readOnly}`** in implementation contexts) means you cannot modify the instance of association or add more instances to it

the `{addonly}` is extremely similar to `{fronzen}` except that you can add more associations to it BUT you cannot modify existing accosiations

## Ordered and unique

from their name they are self explanatory. The `{ordered}` constraint signifies that the elements in the association are ordered and is usually represented by an ordered collection like a list. The `{unique}` signifies that there are no duplicate elements in the association.

## Inhertiance/generalization constraints 

### Disjoint

The Disjoint constraint specifies that the subclasses in a generalization set must be **mutually exclusive**.

- **Rule:** An object instance from the superclass (e.g., `Person`) can belong to **at most one** of the specialized subclasses.
- **Implication:** If an instance is a `Male Person`, it **cannot** simultaneously be a `Female Person`.

### Complete Constraint (`{complete}`)

- **Rule:** The set of subclasses listed in the generalization **is exhaustive** (complete). No other specialized subclasses can be added to this hierarchy.
- **Implication:** Every instance of the superclass _must_ belong to one of the subclasses listed.

### Incomplete Constraint (`{incomplete}`)

- **Rule:** The set of subclasses listed is **not exhaustive**. There are other possible subclasses that could exist or be added later.
- **Implication:** An instance of the superclass might **not** belong to any of the listed subclasses.
- **Example:**  The subclasses "Math", "History", and "Geography" represent an incomplete generalization (meaning more subjects can be added later on).

![[image-75.png]]

## Custom constraints

we can also specify custom constrains that are only relative to that association

![[image-77.png]]

# Example

![[image-69.png]]

