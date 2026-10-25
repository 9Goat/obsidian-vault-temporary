
he Participant Class Diagram is a bridge between the user's needs (Use Cases) and the actual code. It describes, for each specific use case, which classes are needed and how they talk to each other.

To keep things organized, UML uses three specific types of classes (often called **Jacobson Stereotypes**) based on the **MVC (Model-View-Controller)** pattern:

- **Dialogues (Boundary/View)**
- **Contrôles (Controller)**
- **Entités (Entity/Model)**

![[image-314.png]]

# Boundary 

##  What are they?

Boundaries, also called **Dialogues**, **Views**, or **Interfaces**, represent the "skin" of your system. They are the classes that allow interactions between the **Human-Machine Interface (HMI)** and the **Users (Actors)**.

- **Their Role:** They capture everything the user sees and interacts with.
- **What’s inside them?**
    - **Attributes:** These represent data entry fields (like a search bar) or display results (like a list of books).
    - **Operations:** These represent the actions a user performs on the interface, such as clicking a "Search" or "Validate" button.
- **A Key Rule:** Actors can **only** talk to Boundary classes.

## How to figure out what they are

While Boundaries are formally defined in Phase 2, the information comes directly from **Phase 1 (Specification of Needs)**:

- **The Maquette (Mockup):** **One major screen or interface element in your mockup = One Boundary class in your DCP.**
- **The Use Case Diagram:** Each boundary class is always related to a specific **Use Case**. For every oval in your Use Case diagram, you will likely need one or more Boundary classes to facilitate that goal.
- **System Sequence Diagram (DSS):** The DSS shows the chronological flow of messages between the Actor and the System. Every time the Actor sends a message (like `rechercheRapide(motsClés)`), that message must be received by a specific **Boundary** class in your later analysis.

# Controls (Contrôles)

## What are they?

**Their Role:** They contain the "Business Rules" and the logic of the application. They take a request from a Boundary screen (like clicking "Search"), decide what needs to happen, and then ask the Entities (the data) for the information.

**The "Middleman" Rule:** Controls are the only classes that can talk to **everyone**—they can send messages to Boundaries, Entities, or even other Controls.


## How to figure out what they are

- **Rule of thumb (One UC = One Control):** In most cases, you create **one Control class for each Use Case**.
    - _Example:_ For the use case "Gérer son panier," you create a control class named `ctrlPanier`.
- **Splitting for Complexity:** If a use case involves very different types of logic, you can split it into multiple controls to keep it organized.
    - _Example from sources:_ For "Chercher des ouvrages," the logic is split into `ctrlRecherche` (to search the whole catalog) and `ctrlLivre` (to handle specific details of one book).
- **Identifying Operations:** Look at your sequence diagram. Every arrow that was pointing to the "System"  in Phase 1 now becomes an **operation** inside your Control class in Phase 2

# Entities (Entités)

## What are they?

- **Their Role:** They represent the information that the system must store and manage. Unlike other classes, Entities are **persistent**, meaning the information they hold (like a customer's name or a book's price) survives even after the user closes the application or the specific use case ends.
- **What’s inside them?**
    - **Attributes Only:** Just like in the Domain Model, Entity classes in the analysis phase **only contain attributes**. They describe the state of the data (e.g., a `Livre` has an `isbn`, `title`, and `price`).
    - **No Operations:** They do not contain business logic or operations; those belong in the Control classes.

## How to figure out what they are 

- **Direct Source:** Entities are derived directly from the **Domain Model** (Modèle du Domaine) that you created earlier in the analysis phase.
- **Selection:** For a specific Use Case, you simply "pick" the classes from your Domain Model that are needed to perform that action.
    - _Example:_ In the DCP for **"Chercher des ouvrages"** (Search for books), you will include Entities like `Catalogue`, `Livre`, `Auteur`, and `Thème` because the system needs to access that data to show search results.

# Connections

In a correctly modeled system, there are strict rules about who can talk to whom:

- **Dialogue** ↔ **Control:** OK. The screen tells the controller a button was clicked.
- **Control** ↔ **Entity:** OK. The controller asks the entity for information.
- **Dialogue** → **Entity:** **FORBIDDEN.** A screen should never talk directly to the database; it must always go through a controller.

**Note**: the connection between entities in the domain modal **REMAINS** the same in the DCP

#  Example

![[image-315.png]]

