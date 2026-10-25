
# What is an information system?

an **Information System (IS)** is not just servers and code. It is a complex ecosystem made of four key "ingredients"

- **Data**: The raw facts and numbers, like customer names or sales figures.
- **Processes**: The steps that transform data into useful info, such as calculating totals or generating reports.
- **Actors**: People (users, managers) or machines (servers, apps) that interact with the system.
- **Business Rules(regles metier)**: The "laws" that guide it, like "no order ships without payment."

# What is a model

When we model a system like _jeBouquine.com_, we look at it through three different **levels of abstraction**:

- **Niveau Conceptuel (The "What"):** At this level, we describe the intentions and the basic needs of the business.
    - _Example:_ "The system must allow a user to pay for their books".
- **Niveau Logique (The "How"):** We structure the organization of the system but still stay independent of any specific technology.
    - _Example:_ "A 'Payment' class communicates with a 'Bank' class".
- **Niveau Physique (The "With What"):** We specify the exact implementation details and technical tools used to build it.
    - _Example:_ "Using a Java REST API with a PostgreSQL database".

# What is UML

UML is **not a programming language** (like Java or Python) and it is **not a method**—it doesn't tell you _what_ to do first, but it gives you the tools to draw your plans.

To understand a system completely, you can't just look at one drawing. UML allows us to see the system through **three different perspectives (Views)**:

1. **Functional View (The User's Perspective):** This describes what the system does for the person using it.
    - _Analogy:_ Looking at the buttons on a microwave to see what it can do (popcorn, defrost, start).
    - _Main Diagram:_ **Use Case Diagram**.
2. **Static View (The Architect's Perspective):** This describes how the system is built—its structure and parts.
    - _Analogy:_ Looking at the internal components of the microwave (the magnetron, the wiring, the turntable).
    - _Main Diagram:_ **Class Diagram**.
3. **Dynamic View (The Developer's Perspective):** This describes how the parts move and interact over time.
    - _Analogy:_ A step-by-step diagram of how electricity flows and the fan turns once you press "Start."
    - _Main Diagram:_ **Sequence Diagram** or **State Diagram**.

# 5 phases of development

when developing a new application there are 5 main phases that we have to go through before deployment which are the following:

- Spécification des besoins (Requirements Specification)
	- This is the "What" phase. Before writing a single line of code, you must define exactly what the application is supposed to do.
- Analyse (Analysis)
	- In this phase, you break down the requirements to understand the logic and feasibility.
- Conception (Design)
	- This is the "How" phase. you define exactly how your application is going to function with diagrams like sequence diagram
- Implémentation (Implementation / Coding)
	- this is where the actual coding happens, we take all of the diagrams we drawn and turn them into functional  code
- Tests (Testing)
	- Before the app reaches the user, it must be poked and prodded to find "bugs" (errors).

