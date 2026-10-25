sometimes the name of the usecase is not enough to describe enough information about the use case that is why we write a description for it

This description composes of 3 main parts which are:

- identifier
- scenarios description
- alternative sequences

# Identifier

- **Case name**: the name of the use case *example: buy items*
- **Objective:** what is the use case trying to achieve
- **Actors:** actors that are connected to this use case,you have to specify which of those actors are secondary
- **Date**: there are 2 possible date you can set up
	- **Creation date**
	- **last update date**
- **Responsible:** the person who is responsible for it
- **Version**: the current version of the use case

# Description of scenarios

- **Preconditions**: what are the requirements needed for this use case to be viable? What does the user have to do to before initiating this use case?
- **Postcondition:** is the conclusion of the use case. What is the state of the system **AFTER** the use case?
- **Normal scenario**: basically  a table that contains the sequence of actions between both the actors  and the systems during the use case

# Alternative sequences

- **Alternative Flows**: we call few sequences of actions from the normal scenario **BUT** we specify an exception that will result in an alternative sequence.and we have to specify how the system is going to handle this exception.
- **Alternative errors** the same applies to this but in the context of when an error occurs not an unexpected situation

we write the alternative sequences in a list where A number means its an alternative flows **BUT** E number means its an error flow

# Example

here is an example of a **online library system** where the user wants to borrow a book from the librarian

![[image-34.png]]

## identifier

 **Case name**: Borrow book
- **Objective:** Allow a **Member** to check out an available book and update the system records.
- **Actors:** Member,librarian(Secondary)
- **Date**: there are not information to provide for this but if there are provide them
	- **Creation date**
	- **last update date**
- **Version**: 

## Description of scenarios

- **Preconditions**: The Member must be logged into the system. The desired book must be marked as "Available" in the catalog.
- **Postcondition:**: The book is marked as "On Loan" to the Member, and a due date is recorded.
- **Normal scenario**: the normal scenario can be a straight list 

1. The use case begins when the **Member** finds a desired available book in the system (e.g., via the Search Catalog use case) and selects the "**Borrow**" option.
2. The **System** verifies that the Member's account is in good standing (no maximum book limit reached, no overdue books).
3. The **System** verifies that a copy of the selected book is currently available.
4. The **System** reserves the book for the Member, records a due date, and updates the status of the book to "**On Loan**."
5. The **System** displays a confirmation message to the Member, including the due date.
6. The use case ends.

or it can be written in the for of a table where there are no table headings (the first column describes the sequences handled by the actors and they other column describes those handled by the system itself)


| 1. The use case begins when the **Member** finds a desired available book in the system (e.g., via the Search Catalog use case) and selects the "**Borrow**" option. | 2. The **System** verifies that the Member's account is in good standing (no maximum book limit reached, no overdue books).      |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
|                                                                                                                                                                      | 3. The **System** verifies that a copy of the selected book is currently available.<br>                                          |
|                                                                                                                                                                      | 4. The **System** reserves the book for the Member, records a due date, and updates the status of the book to "**On Loan**."<br> |
|                                                                                                                                                                      | 5. The **System** displays a confirmation message to the Member, including the due date.                                         |
| 6. The **Member** takes the book he borrowed                                                                                                                         |                                                                                                                                  |

## Alternative sequences

- **Alternative flows**

1. **A1: Book is Unavailable**, starting step 3,If the System finds that no copies are available, the System prompts the Member to place a **Hold Request** on the book. 
2. **A2: Maximum Limit Reached**, starting step 2,If the System finds the Member has reached their borrowing limit, the System informs the Member of the limit and lists their currently borrowed books.

- **Error flows**

1. **E1: Account Overdue**,starting step 2,If the System finds the Member has overdue books, the System blocks the request, informs the Member of the overdue items, and the use case terminates in failure.

# Notes

- we have to **START** each scenario with the name of the actor
	 - **Example**: The user enters his login information
		- the bank process the login detaills,,,,etc

