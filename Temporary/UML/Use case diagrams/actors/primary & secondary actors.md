
# Primary

an actor is called primary if it is the one to **initialise** a system.they are **ALWAYS** placed to the left of a system

## Example

The primary actor for an **ATM system** is the **Bank Customer**.

- **Why?** The customer is the one who initiates the main goal: **Withdrawing Cash**.

# Secondary

an actor is called secondary if it is the one that the system needs to accomplish the goal initiated by the primary actor, often providing or receiving information. they are **ALWAYS** placed to the right of a system

## Example

For the **ATM system**, the **Bank's Server** is a secondary actor.

- **Why?** The Bank's Server is used by the ATM system to verify the customer's account details and complete the transaction initiated by the primary actor


# Example

both the secondary and the primary actors are presented with the keywords `<<primary>>` and `<<secondary>>` in their connections with the use case

![[image-15.png]]