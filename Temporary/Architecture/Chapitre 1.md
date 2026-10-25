
# 3 Levels of abstraction

A software application is typically divided into three distinct functional levels:

![[image-266.png]]

## 1. The Presentation Layer (IHM)

- **Definition:** Also known as the Human-Machine Interface (IHM in French), this is the topmost layer that interacts directly with the user.
- **Responsibilities:** It handles keyboard inputs, mouse actions, and displaying information on the screen for the user (basically what the user interacts with.
- **Example:** When you use a banking app, the screen where you type your username and view your balance is the Presentation Layer.

## 2. The Application Layer (Logic/Business Layer)

This layer is divided into two sub-types of processing:

- **Local Processing:** These are controls tied to the interface dialogue, ensuring data is consistent between what the user sees and the system logic.
- **Example (E-commerce):** When you fill out a shipping form, if you leave the "Email" field blank or type "12345" as your name, the Application Layer catches this immediately and shows a red error message. It doesn't need to ask the database if your name is valid; it knows based on local rules.
- **Global Processing (Business Logic):** This represents the "intelligence" of the application. It contains the internal rules that govern how a business or system operates.
- **Example:** In that same banking app, the rule that says "You cannot withdraw more money than your current balance" is part of the Business Logic.

##  **3. The Data Layer**

- **Definition:** This is the bottom layer, specifically focusing on **data access**.
- **Responsibilities:** It groups all mechanisms used to manage and store the information used by the application.
- **Example:** The physical database where your actual account balance (e.g., "$1,250.00") is stored and the code that retrieves it.

# 1 Tier architecture

A **1-tier application** is one where all three layers  are used and executed on the **same computer**. This is referred to as **centralized computing** rather than a client-server model.

There are two main historical types of 1-tier architecture:

![[image-267.png]]

## 1. Centralized 1-Tier (The Mainframe Era)

In this setup, there is only **one brain**. That brain is a massive central computer called a **Mainframe**.

- **How it works:** All three layers (Presentation, Application, Data) live and breathe on the Mainframe.
- **The User's Device:** Users sit at "Passive Terminals" (Dumb Terminals). These have no CPU or hard drive. They are essentially just a monitor and a keyboard. When you type a key, it is sent to the Mainframe; the Mainframe decides what to do and sends back a character to display on your screen.
- **Analogy:** It’s like using a "Remote Desktop" , but for old-school text-based software. The user's machine is just a "window" into the server.
- **Pros:** Very reliable, and uses resources optimally since power is concentrated in one machine.
- **Cons:** Uses old interfaces (like an old command prompt) which are considered obsolete.

## 2. Distributed 1-Tier 

As PCs became powerful enough to have their own "brains," the model changed. Now, the application is actually installed on each user's computer.

- **How it works:** Applications are installed on independent PCs. Users share data files stored on a common server, but each client PC runs its own database engine.
- **The Big Difference:** Unlike the centralized model, the "File Server" doesn't do any thinking. It is just a hard drive attached to a network cable. When a user wants to search for a customer name, their PC has to download the _entire_ customer file from the server, search it locally, and then send it back.
- **Pros:** Better interface (GUI).
- **Cons:** Can saturate the network because files are constantly being moved back and forth, and data security/confidentiality is harder to manage.

|**Feature**|**Centralized 1-Tier**|**Distributed 1-Tier**|
|---|---|---|
|**Where does the code run?**|On the Mainframe (Server).|On the User's PC (Client).|
|**User Device Power**|Low (Passive Terminal).|High (Workstation/PC).|
|**Network Traffic**|Very Low (only sends keystrokes).|Very High (sends entire data files).|
|**User Interface**|Text-based (Green screens).|Graphical (Windows/Icons/Mouse).|
|**Security**|Very High (nothing leaves the server).|Lower (data travels across the network).|

# The 2-Tier Architecture (Client-Server)

In a 2-tier architecture, the workload is split between two distinct components connected via a network: the **Client** and the **Server**.

![[image-268.png]]

## The Division of Labor

Unlike the 1-tier distributed model (where the server was just a "passive" file holder), the server in a 2-tier model is **active**.

- **The Client:** Handles the **Presentation Layer** (the UI) and parts of the **Application Layer**.
- **The Server:** Handles the **Data Layer** (DBMS). It processes queries (like SQL) and only sends the _result_ back to the client, not the whole file.

## Middle ware

To make this Client-Server communication possible, we need a "bridge."

### What is a Socket?

A socket is the technical endpoint for communication. It is defined by two things:

1. **IP Address:** The address of the machine (e.g., `192.168.1.50`).
2. **Port Number:** The "door" to the specific service (e.g., Port `80` for Web or `1521` for Oracle).

### What is Middleware?

Middleware is a software layer that sits **above** the socket. Its purpose is to hide the complexity of the network from the developer.

If the socket is the telephone wire, the **Middleware is the translator** on the other end of the line who speaks both languages and handles the paperwork.

- **Transparency:** You don't need to know _where_ the server is or _how_ it stores data. You just ask the middleware for the information, and it finds it for you.
- **Standardization:** It provides a common set of rules (APIs) so that different applications can communicate regardless of their underlying technology.


## Fat client

The client is is called **Fat client in the 2-tier architecture**

**Fat Client (Client Lourd):**

- The user's PC does almost all the "thinking."
- It contains the UI + Local Processing + **Global Business Rules**.
- The Server is only used for data storage/retrieval.
- _Problem:_ If you change a business rule, you must reinstall the app on every single computer.

### **Advantages & Disadvantages of 2-Tier**

- **Advantages:**
    - **Reduced Network Traffic:** Only the necessary data is sent (e.g., 1 row of a table) instead of the whole file.
- **Disadvantages:**
    - **Scalability:** If too many clients connect at once, the DBMS server gets overwhelmed because it has to maintain a constant connection with every single client(we CANNOT add more dbms servers because  it creates a problem of which  user talks to  which database and creates possible data mismatch problems).


# The 3-tier architecture

The 3-tier architecture was designed to solve the "Fat Client" and "Maintenance" problems of the 2-tier model. In this setup, we introduce a third, middle machine.

![[image-269.png]]

## The three layers

Instead of just a Client and a Server, we now have:

- **Tier 1: The Client (Presentation)**
    - This is now a **Thin Client** (usually a web browser).
    - It _only_ handles the display and very basic input validation (Local Processing).
- **Tier 2: The Application Server (Logic/Middleware)**
    - **This is the most important change.** All the **Global Business Rules** and **Middleware** are moved here.
    - When the client needs something, it asks the Application Server. The Application Server then processes the logic and asks the Database for data.
- **Tier 3: The Data Server (Data)**
    - The database engine stays here, but it only talks to the Application Server, never directly to the client.

| **Advantages**                                                                       | **Disadvantages**                                                                                                    |
| ------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------- |
| **Highest Scalability:** Best for systems with thousands of simultaneous users.      | **Complexity:** Much harder to configure and deploy than a 1-tier or 2-tier system.                                  |
| **High Availability:** If one server in a specific tier fails, others can take over. | **Network Latency:** Since data has to travel through many "stops" (tiers), it can be slower if the network is weak. |
| **Security:** Each tier acts as a firewall for the next one.                         | **Cost:** Requires more hardware and specialized maintenance.                                                        |

## The Web-Based 3-Tier Model

![[image-265.png]]

1. **The First Tier: The Web Browser (Thin Client)**
    - In this "Web 3-tier" version, the presentation layer is handled entirely by a **standard web browser** (like Chrome, Firefox, or Safari).
    - The browser's only job is to receive HTML/CSS/JavaScript from the server and display it to you. It does not store the "rules" of the application.
2. **The Second Tier: The Web/Application Server (HTTP/Logic)**
    - This is the middleman. It receives requests from your browser via the **HTTP protocol**.
    - It contains the **Business Logic** (Global Processing) and uses technologies like Java , PHP, or Python to process your request.
    - It acts as the "brain" that decides what data is needed from the database.
3. **The Third Tier: The Database Server**
    - The database remains the final destination where the actual data is stored (SQL Server, Oracle, MySQL, etc.).
    - The Web Server (Tier 2) talks to the Database (Tier 3), gets the results, and then sends them back to your browser as a webpage.

### **Why the "Web" makes 3-Tier powerful:**

- **Zero Installation:** Unlike the 2-tier "Fat Client," the user doesn't need to install any special software. As long as they have a browser, they can use the app.
- **Universal Access:** The application can be accessed from any device (PC, phone, tablet) because the "Logic" is centralized on the web server.
- **Scalability:** If millions of people visit the site, you can simply add more Web Servers (Tier 2) to handle the traffic without ever touching the Database or the Client's computer.

in the 3 tiers the client is referred to as thin client:

**Thin Client (Client Léger):**

- The user's PC only handles the UI and basic validation.
- The **Global Business Rules** are moved to the Server (often using "Stored Procedures" in the database).
- _Benefit:_ Centralized logic is easier to update.

# n tiers

![[image-270.png]]

This is simply a 3-tier architecture where the middle layer (Tier 2) is broken into even more pieces.

- **Example:** You might have one server just for Security, one for the Shopping Cart logic, and one for the Payment Processing.
- **Why use it?** If the "Payment" part of your code gets millions of hits but the "Shopping Cart" doesn't, you can add more servers _only_ for the payments. 

![[image-271.png]]


## 1. RPC (Remote Procedure Call)

- **The Concept:**  It allows a computer program to cause a  procedure to execute in another place (commonly on another computer on a shared network/severs).The programmer doesn't have to worry about the **network code** (IPs, packets, or connection logic). To the programmer, it looks like a local call.
- **How it works:** To the programmer, it looks like they are calling a local function (e.g., `calculateTax()`). However, the RPC middleware intercepts that call, sends it over the network to a remote server, gets the result, and hands it back to the local program.
- **Key takeaway:** RPC is **procedural**. It’s about calling "functions" or "methods" across the network.

## 2. ORB (Object Request Broker)

- **The Concept:** This is the "Object-Oriented" evolution of RPC. As software moved from procedural languages (like C) to Object-Oriented languages (like Java), we needed a way to talk to **Objects** on other servers.
- **The Role:** The ORB acts as a "broker" or a "bus." When a client object wants to interact with a server object, it sends a request to the ORB. The ORB finds the object on the network, delivers the request, and returns the result.
- **Key takeaway:** ORB is **object-oriented**. It allows objects to interact regardless of what language they are written in or what OS they run on.