The Use Case Diagram is the starting point of the **Requirement Specification phase** (Spécification des besoins). Its goal is simple: to show **"What"** the system does from the perspective of an external observer, without worrying about the internal code.

# 6 steps to build a use case diagram

- **Identify the System Boundaries (Identifier les limites du système):** You must clearly define what is part of your application (inside the box) and what is external to it.
- **Identify the Actors (Identifier les acteurs):** You look for anything external—human or machine—that interacts with the system.
    - _Example from the sources:_ Human actors like the **Internaute** or **Webmaster**, and system actors like **Paiement sécurisé**.
- **Identify the Use Cases (Identifier les cas d'utilisation):** You list the specific goals the actors want to achieve.
    - _Example:_ "Chercher des ouvrages" or "Passer une commande".
- **Structure Use Cases into Packages (Structurer en packages)  OPTIONAL:** For large systems, you group related use cases together to keep the diagram readable.
    - _Example:_ Creating a package for "UC des clients" and another for "UC des employés".
- **Add Relationships (Ajouter les relations):** This is where you connect actors to use cases and define links between use cases using `<<include>>`, `<<extend>>`, or generalization.
- **Classify Use Cases (Classer les cas d'utilisation):** You prioritize or rank the use cases (e.g., "Primary" vs "Secondary" rank) to help plan the development phases.


# Actual Construction of the Use Case Diagram

we will be creating the overall use case diagram of the application alongside the textuelle description

content can be found in my use case diagrams folder


