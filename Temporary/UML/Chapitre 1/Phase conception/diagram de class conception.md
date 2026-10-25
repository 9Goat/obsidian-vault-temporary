
The Design phase is where we stop talking in "business terms" and start talking in "coding terms". Its goal is to fix technical choices and create the final blueprint that a developer can use to write the code.

# The diagram

The Design Class Diagram (DCD) is not a new diagram; it is an **evolution** of the Participant Class Diagram (DCP) you made in analysis. You take your Boundaries, Controls, and Entities and "dress them up" with technical details.

basically you turn the simple [[Participant class diagram]] and turn  them into a class diagram:

- boundaries:
	- **attributes**: they can contain attributes just like entities and their attributes can be labelled with `<<resultat>>` if that attribute is the resulted of an operation like (show the number of pages with an attribute called nbPages)
	- **methods**: since they represent pages of the application that means they can contain methods when the user performs a specific action like  submit form
- controles:
	- **methods**: they only contain methods 
- entities:
	- **attributes**: they only contain information about themselves

## Example

**FROM THIS DCP**

![[image-329.png]]

**TO THIS**

![[image-330.png]]