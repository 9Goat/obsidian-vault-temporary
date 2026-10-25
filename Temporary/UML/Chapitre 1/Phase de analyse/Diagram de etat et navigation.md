# State diagram

While the Class Diagram shows what the system **is**, the State Diagram shows how a specific object **acts** during its entire life.

## 1. What is it?

It is a diagram that describes the different "states" an object can be in and the "events" that cause it to change from one state to another.

- **A State (État):** A condition or situation in the life of an object (e.g., an order is "Paid").
- **A Transition:** A relationship between two states indicating that an object in the first state will enter the second state when a specific event occurs (e.g., the "payment" event moves an order from "Validated" to "Paid").

## 2. How do we figure out what needs a State Diagram?

According to your sources, it is **not necessary** to create a state diagram for every entity in your system.

- **The Rule:** You only create one for entities that have a **complex dynamic behavior** that needs a detailed description.
- **Example:** In the _jeBouquine.com_ system, most entities like `Livre` (Book) or `Auteur` (Author) are simple data. However, the **Commande** **(Order)** class is complex because it goes through many stages (creation, validation, payment, preparation, delivery).

## 3. Examples

to draw them we need to check the folder that contains info about how to create them

**We will be creating the states diagrams where one shows the normal state where no alternatives occur and an another where an alternative occurrs**

![[image-325.png]]

![[image-326.png]]

# Navigation diagram

While the State Diagram shows the life of a data object (like an Order), the **Navigation Diagram** shows the life of a user’s session. It formally represents all the possible paths a user can take between the different screens of the application.

## 1. What is its purpose?

- It provides a dynamic view of the **Human-Machine Interface (HMI)**.
- It helps developers understand the "flow" of the website—how a user gets from the Home Page to a Book Detail page, and finally to the Payment screen.

## 2. What are its components?

- **Nodes (Screens):** Represented as boxes with stereotypes like `«page»` (a full web page) or `«frame»` (a part of a page, like the search results section).
	- Basically instead of states we have pages and frames from out website
- **Transitions (Arrows):** the same format of transitions as [[Transitions]]
    - _Example:_ From the `Page d'accueil` (Home Page), a user can trigger a `recherche rapide` to move to the `Résultat de la recherche`.
- **Special Elements:** It can also show `«connector»` elements (like the Panier/Basket that ) that act as hubs, or `«exception»` nodes to handle errors like "No books found".
	- a `«connector»` is used to simplify the diagram by showing a component or a destination that can be reached from **many different places** in the application.

## Example

![[image-328.png]]