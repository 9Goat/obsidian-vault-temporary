
# Actors generalisation

there is only a single relationship between actors which is **`generalisation`** 

## Explanation

an actor **A** is called a **`generalisation`** of actor **B** only if actor **A** can:

- be substituted by actor B 
- all use cases accessible to A are also accessible to B
- but the reverse is **NOT** true.

the **`generalisation`** is demonstrated with a straight arrow that has a **NON FILLED** triangular ending --|> from the actor that is being substituted to the specific actor

## Example

-  **General Actor (Parent):** Teacher
- **Specific Actor (Child):** Substitute Teacher

![[image-27.png]]

# use case generalization

the same thing also applies to use cases so we are not going to be explaining but instead just provide an example

## Example

Imagine an ATM system where the core, high-level function is **Withdraw Funds**. Two distinct, specific ways the customer can achieve this goal are Fast Cash Withdrawal and Custom Amount Withdrawal.

- **General Use Case (Parent):** Withdraw Funds
- **Specific Use Case (Child 1):** Fast Cash Withdrawal
- **Specific Use Case (Child 2):** Custom Amount Withdrawal

The relationships are read as:

1. **"Fast Cash Withdrawal is a type of Withdraw Funds."**
2. **"Custom Amount Withdrawal is a type of Withdraw Funds."**

![[image-28.png]]