# Definition

- **French**: Un acteurs est une entité extérieure au système modélisé, et qui interagit directement avec lui.
	- il peut consulter et/ou modifier l’état du système par messages

- **English**:An actor is an entity external to the modeled system, and which interacts directly with it.
	- he can consult and/or modify the state of the system by messages

most of the times actors are one of the following:

- Person/user
- Organization
- another system
- an external device

## Representation

![[image-14.png]]

# Notes

- actors **MUST** atleast be connected to a single use case , but the opposite is not true use cases can be connected to other uses cases
- when naming actors we need to treat them as types or categories **NOT** a real world example
	- meaning instead of naming an actor **John** to represent a user we can just call him **Customer or User**