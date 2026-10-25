# Types of structures

##  N tiers

┌─────────────────────────────────────┐
│         Niveau 3 (Level 3)          │
│         Composant 3.1               │
├─────────────────────────────────────┤
│         Niveau 2 (Level 2)          │
│   Composant 2.1  │  Composant 2.2   │
├─────────────────────────────────────┤
│         Niveau 1 (Level 1)          │
│   Composant 1.1  │  Composant 1.2   │
└─────────────────────────────────────┘

### **What is it?**

- **Vertical organization** of the system
- Components are arranged in layers/tiers
- Each layer has a specific level of abstraction and responsibility

### **When to use it?**

When you have **multiple levels of abstraction** in responsibilities:

- **Upper layers**: Interact with users (handle requests)
- **Lower layers**: Operate on data (provide responses)

### Recommendations (Best Practices):

1. **Group reusable classes together**
    - A layer should be formed by classes that are reusable under the same conditions
    - Classes with similar abstraction levels belong in the same layer
2. **Use interfaces between layers**
    - Relations between layers are described through interfaces
    - **Goal**: Create "firewalls" between layers
    - Changes in one layer don't affect others if the interface stays the same
3. **No component spans two layers**
    - Each component belongs to exactly ONE layer
    - No straddling between layers
4. **Communication limited to consecutive layers**
    - Layer 3 talks to Layer 2
    - Layer 2 talks to Layer 1
    - Layer 3 does NOT directly talk to Layer 1

### Advantages:

✅ **Reusable and interchangeable layers**

- You can swap out a layer if you need to (as long as interface is maintained)

✅ **Only local dependencies**

- Dependencies exist only between two consecutive layers
- Changes are isolated and don't ripple through the entire system

✅ **Developers can ignore other layers**

- Developers working on Layer 2 don't need to understand Layer 1 or Layer 3 internals
- Everything happens through interfaces
- Users of each layer only need to know the interface, not the implementation

## 3 tiers

┌────────────────────────────────────────┐
│   Niveau Présentation (Presentation)   │
│      Interface Utilisateur (UI)        │
│   • Visualizes data                    │
│   • Presentation logic                 │
└────────────────────────────────────────┘
              ↕️ Query
┌────────────────────────────────────────┐
│   Niveau Application (Application)     │
│      Règles Métier (Business Rules)    │
│   • Coordinates decisions              │
│   • Logical evaluations                │
│   • Performs calculations              │
└────────────────────────────────────────┘
              ↕️ Data requests
┌────────────────────────────────────────┐
│     Niveau Données (Data Layer)                                                               │
│           ORM (Database)                                                                                  │
│   • Data storage                                                                                              │
│   • Data retrieval from databases                                                             │
└────────────────────────────────────────┘

### **Flow Example (from the diagram):**

**User request**: "GET LIST OF ALL SALES MADE LAST YEAR"

1. **Presentation Layer** receives the request
2. Sends query to **Application Layer**: "get SALES TOTAL"
3. **Application Layer** asks **Data Layer** for data: "SALE 1, SALE 2, SALE 3, SALE 4"
4. **Application Layer** performs calculation: "ADD ALL SALES TOGETHER"
5. Returns result to **Presentation Layer**: "4 TOTAL SALES"
6. **Presentation Layer** displays to user

## Pipes and filters

```
Input → [Filtre 1] → [Filtre 2] → [Filtre 3] → [Filtre 4] → Output
        ───────────  ───────────  ───────────  ───────────
           Pipe         Pipe         Pipe         Pipe
```

### What is it?

- **Horizontal organization** (not vertical like N-Tier!)
- Data flows through a series of processing steps
- Each step transforms the data in some way

### Components:

1. **Filters** (Filtres):
    - Independent processing components
    - Each filter performs ONE specific transformation
    - Encapsulates one step of the processing
2. **Pipes** (Tubes):
    - Connections between filters
    - Transport data from one filter to the next
    - Typically implemented as Unix pipes or files




# The MVC Pattern

![[image-280.png]]

The goal of MVC is to separate the **Internal Logic** from the **User Interface**. This ensures that if you change how the data looks (the View), you don't have to change how the data is processed (the Model).

It is divided into three distinct parts:

1. **The Model (Le Modèle):**
    - **Role:** This is the "Heart" of the application. It manages the data, the business rules, and the state of the system.
    - **Rule:** It is independent of the interface. It doesn't know if the data will be shown on a website, a mobile app, or a terminal.
2. **The View (La Vue):**
    - **Role:** This is the "Face" of the application. It represents the data from the Model to the user (e.g., a chart, a table, or a form).
    - **Rule:** It should not contain any business logic. It just displays what it is told.
    - **Automatic Updates:** When the Model changes, it sends a notification to the View, and the View updates itself automatically.
3. **The Controller (Le Contrôleur):**
    - **Role:** This is the "Brain" or "Manager." It receives input from the user (clicks, typing, gestures), translates them into actions for the Model, and chooses which View to show next.

## Advantages

- the views and the model can evolve independently
- Multiple views on the same model. 
- A view can be easily added.

## Disadvantages 
- The view has two responsibilities: displaying and retrieving data. 
- Difficult to test.

## Example

- **The Model (The Kitchen):** The chefs prepare the food and manage the ingredients. They don't care who is sitting at table 5; they only care about making the recipe correctly.
- **The View (The Plate):** This is how the food is presented to the customer. The same "Steak" (Model data) can be presented on a fancy plate or in a plastic take-away box (different Views).
- **The Controller (The Waiter):** The waiter takes your order (User Input), tells the kitchen what to cook (Update Model), and then brings the correct plate back to your table (Update View).

# The MVP Pattern (Model-View-Presenter)

![[image-281.png]]

In the classic MVC we just studied, the View and the Model can sometimes talk to each other (the View "observes" the Model). **MVP** changes this to make the code even cleaner and more testable.

- **The Model:** Still exactly the same (Data and Logic).
- **The View:** Still the UI, but it is now **Passive**. It doesn't do anything except display what it is told.
- **The Presenter (The "Middle-Man"):** This replaces the Controller.
    - **The Big Change:** In MVP, the View and Model **never** talk to each other. They are completely separated.
    - The Presenter acts as a 2-way bridge. It fetches data from the Model, formats it into a simple string, and hands it to the View.

## Advantages

- Eliminates interaction between the view and the model.
- Interaction is handled through the presentation, which organizes the data to be displayed in the view.
- Everything is testable except the view, but it lacks logic.
- The model is independent of other components.

## Disadvantages

- A lot of redundant code (boilerplate code) in the presentation to update the data in the view, such as: 
	- displayText1(text), displayText2(text) 
	- setButton1Enabled(true), setButton2Enabled(true)

## Example

- **The Model (The Kitchen):** Prepares the food.
- **The View (The Guest):** Sits in the room. They never see the kitchen.
- **The Presenter (The Butler):** The guest tells the butler they are hungry. The butler goes to the kitchen, gets the food, puts it on a specific tray that fits the guest's table, and delivers it.
    - _Why is this MVP?_ If the guest wants the food chopped into small pieces, the **Butler** (Presenter) does that before the Guest (View) sees it. The Kitchen (Model) just provides the raw steak.

# The MVVM Pattern (Model-View-ViewModel)

![[image-282.png]]


This is the standard for modern frameworks (like **Vue.js**) . It introduces a revolutionary concept called **Data Binding**.

1. **The Model:** Still the same (Data and Business Logic).
2. **The View:** The UI (HTML/CSS/XML).
3. **The ViewModel:**
    - **The Key Difference:** In MVP, the Presenter had to manually say `view.setText("Hello")`. In MVVM, the ViewModel doesn't talk to the View at all.
    - Instead, the View is **"Bound"** to the ViewModel.
    - **Data Binding:** Think of it like a "Live Sync." If a variable `name` changes in the ViewModel, the text on the screen changes **automatically** without any extra code.

## Advantages

- **Eliminates "Boilerplate" Code:** You don't have to write hundreds of `setText()` or `updateUI()` methods. The "Binder" (the framework) handles the sync for you.
- **Reusability:** A single ViewModel can often be used by multiple different Views because it just exposes "properties" of data.

## disadvantages

- Data binding can lead to considerable resource consumption.
- over complication of using many variables
- not all graphic libraries support data binding

### **The "Evolution" Summary**

- **MVC:** The View watches the Model.
- **MVP:** The Presenter manually moves data between the two.
- **MVVM:** The View and ViewModel are "synchronized" automatically.


A **monolithic application** is a software architecture where all the components and functions of the system (the user interface, business logic, and data access) are unified into a **single, indivisible unit**.

In this model:

- The entire application is developed, managed, and deployed as one single file (e.g., a `.jar` or `.war` file in Java).
- All functions share the same memory and resources.
- If you need to update one small part (like the CV builder), you must redeploy the entire application.

This is a **2-Tier Architecture** (also known as a classic Client-Server architecture).

**Justification:**

- **Separation of Concerns:** The description mentions "personalized interfaces" for candidates and employers (the **Client/Presentation Tier**) and the ability to "deposit CVs" or "post offers" which involves storage and processing (the **Server/Data Tier**).
    
- **Monolithic Nature:** Since the text explicitly states the application is "monolithic," it implies that the logic and the data handling are tightly coupled on the server side, typically interacting directly with a database.
    
- **Direct Interaction:** In a 2-tier setup, the client (the user interface) communicates directly with the server (the monolith) where the database and business logic reside together.

