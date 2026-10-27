# Services

## Definition

a service is a **software component that performs an action on behalf of a client**. It represents the **logical level** of access to a treatment (what it does), not the **physical level** of implementation (EJB, Servlet...).

## components

- **Shared / mutualised** - reusable and interoperable, so many applications use the same service.
- **Referenced in a directory** (annuaire) - where it is identified and can be found.
- **Standardised** - all functions are called the same way, with parameters, following a **contract**.
- **Described by an interface** - written in a language independent of technologies.
- **Communicating by messages** (inputs/outputs) with the client.
- **Neutral** - its use does not depend on its implementation or evolution, as long as the contract is respected.
- **Loosely coupled** - the interface isolates the client from the service.
- **Deployed physically on a server.**

## service ochestration

Services can be **composed (aggregated)** to carry out a business process. The problem: if every service calls every other service directly, you get a tangled web (**strong coupling**). With **orchestration**, an **orchestration engine** calls the services in the right order, so services can cooperate **without knowing each other** - this keeps their **loose coupling** and independence.

**Strong vs loose coupling (slide idea)**

![[image-445.png]]

##  Service types

  
| **Type**                        | **Role**                                                                                                                                                                                                                                                                                                                                                  | **Examples**                                       |
| ------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------- |
| **Applicatif** (Application)    | Translates the **application logic** / business process. Operations triggered if **preconditions** are true; results emitted if **postconditions** are true. **Context-aware** .Il peut être modélisé par : - UML : Uses cases et Diagramme d’activité<br>- MERISE : Modèle Organisationnel de Traitements<br>- BPMN (Business Process Modeling Notation) | ProcessLoanRequest, OrderCheckout                  |
| **Fonctionnel** (Functional)    | Executes a **business treatment (function)**, reusable in many contexts, called by several application services. Calls CRUD and/or transverse services to handle business objects. Can also handle security and business rules.                                                                                                                           | CalculTVA, CalculRemise, VerificationCredit        |
| **Entité (CRUD)**               | Elementary service to **Create, Read, Update, Delete** a business object (also search or **export** to PDF/Excel).                                                                                                                                                                                                                                        | GestionClient, GestionCompte, GestionProduit       |
| **Transverse** (Infrastructure) | Technical treatment used by everyone (not tied to one business object).                                                                                                                                                                                                                                                                                   | LoggingService, UserContext, Audit, Authentication |
| **Host**                        | Lets distributed applications use an **enterprise Mainframe (Host)** application. Encapsulated in infrastructure software.                                                                                                                                                                                                                                | Wrapper around a COBOL banking transaction         |
**EXAM TIP:** How to classify quickly: **only CRUD on data -> Entity.** **Technical, used everywhere (log, audit, security context) -> Transverse.** **One reusable business computation/rule (tax, discount) -> Functional.** **A whole business process with a flow of steps and pre/post-conditions (loan, order) -> Application.** **Talks to a mainframe -> Host.** Always **justify** in one sentence.
## Service properties

  
| **#** | **Property**                                       | **One-line meaning**                                         |
| ----- | -------------------------------------------------- | ------------------------------------------------------------ |
| 1     | Reusable, with standardised contracts              | Same service used by many consumers, described by a contract |
| 2     | Addressable interfaces + communication by messages | Reachable at a network address; talks only by messages       |
| 3     | Abstract and predictable                           | "Black box"; always behaves the same way                     |
| 4     | Modular and coarse-grained                         | Big grain with coherent interfaces; deployable independently |
| 5     | Autonomous and stateless                           | Independent of others; keeps no client state                 |
| 6     | Interoperable                                      | Works with heterogeneous systems                             |
| 7     | Loosely coupled                                    | Depends on the contract, not on the implementation           |
| 8     | Discoverable (dynamically)                         | Published in a directory, found by criteria                  |
| 9     | Composable                                         | Can take part in compositions / orchestrations               |


### Reusable 

The **contract** describes three things:

- **Syntax:** operations, inputs, outputs, formats, protocol.
- **Semantics:** how to use it - **pre-conditions** and **post-conditions**.
- **QoS (Quality of Service):** expected response time, recovery time after an interruption...

For REST services the contract is described with **WADL**

- Several contracts can exist for one service (e.g. high availability vs normal availability).
- The contract is used at **design-time** (code generation) and at **run-time** (checking that the contract is respected).

### Communication by messages

- A consumer calls the service through its **network address** at any time (if on the same machine it can call it locally to go faster).
- Services communicate **only by messages** - in SOA they are distributed, so each call is a network call.
- To improve performance, make interfaces **coarse-grained**(respondes to request with 1 call needed instead of 3 for example) to **reduce the number of network calls**.

### Abstraction and predictibilty

- **Black box:** the consumer sees only the **contract**. Business logic and implementation are **hidden**.
- **Predictable:** for the same request the behaviour and response do not vary.

### Modularity

- **Coarse granularity:** a service is a big grain grouping a set of coherent interfaces for **one functional module** (a design principle).
- **Modularity:** it can be deployed **atomically**, even before the consuming applications are developed. This differs from OO, where a program is one indivisible unit.

### Statelness

- **Autonomy:** independent of external services; its behaviour does not depend on the functional or technical context of the call.
- **Stateless:** it does **not manage a client context** between calls.
- **Why?** (a) simpler maintenance, (b) keeps **reusability** - independent of any particular sequence of calls, (c) **performance** - no system resources used to store state.

 
|**Stateful (bad for services)**|**Stateless (what we want)**|
|---|---|
|A waiter who **remembers** you: "the usual?" If another waiter takes over, he knows nothing and the order is lost.|You hand over an **order slip with everything written on it** each time. Any waiter can serve you.|
|The server keeps your shopping cart in its memory between two requests.|Each request contains everything needed (who you are + what you want). The server remembers nothing.|
|Server memory is used for every client; clients are tied to one server.|Minimum resources; you can add servers freely.|

### Interporability

- Ability to communicate with a **heterogeneous system** (different languages, platforms).
- The service defines a **connector type** (protocol + data format) that clients must use - e.g. **HTTP + JSON**.
- If the client uses another format, a **mediation** specification does the mapping (e.g. between character sets such as ASCII and EBCDIC, or data-type mapping).

### Loose coupling

- Weak dependency between consumer and service: depends on the **contract**, not on the implementation; exchange via **messages**.
- **Orchestration** guarantees independence: services cooperate without knowing each other.
- **Advantage - easy maintenance:** a change inside the service causes few changes in consumers (only those needed to respect the contract).

### Discoverablity

- The provider **publishes** the service in a **directory/registry** (annuaire) with **metadata** that identifies it (and can be updated).
- The consumer **searches** by criteria; the directory returns the list of matching services (addresses, fees...).
- Everything needed to call it (operations, parameters) is read from its **contract**.

### Composability

- A service can take part in **compositions**: several services are composed through **orchestration** to answer a complex need.
- **Advantages:** **added value** (answers a new complex need) and **more modularity** (a complex service is decomposed into simple services, each deployable atomically).

# HTTP

## Definition

**HTTP = HyperText Transfer Protocol.** A protocol that lets a **client** retrieve **documents** from a **server**, and also submit forms.

- **Static** documents: content does not change (HTML, PDF, images...).
- **Dynamic** documents: generated at request time (PHP, JSP, ASP...).
- Port: the server listens on **port 80** (HTTP) - 443 for HTTPS.

### How it works (simple HTTP/1.0 flow)

1. The client **connects** to the server (creates a socket).
2. The client **sends a request** asking for a document.
3. The server **sends back** the document (status **200**) or an error (status **404** if it does not exist).
4. **Disconnection.**

```text
**HTTP exchange**

CLIENT (browser) SERVER (port 80)

| ---- (1) connection (socket) --------> |

| ---- (2) GET /doc.htm -------------> |

| <--- (3) 200 OK + doc.htm ---------- |

| ---- (4) disconnection -------------> |

```

## HTTP methods

   
|**Method**|**Purpose (from the slides)**|**Safe?***|**Idempotent?****|
|---|---|---|---|
|**GET**|Retrieve the content of a document|Yes|Yes|
|**POST**|Submit forms - send, in the request, data typed by the user (creates)|No|No|
|**PUT**|Send a file/data from client to server (update)|No|Yes|
|**DELETE**|Ask the server to delete a document|No|Yes|
|**HEAD**|Get information about a document (type, size, last modification date...) without the body|Yes|Yes|

**structure of http request**

![[image-446.png]]
**structure of http response**

![[image-447.png]]

### Https status

  
|**Code**|**Meaning**|**Typical use in REST**|
|---|---|---|
|**200** OK|Success|Successful GET, PUT or DELETE|
|**201** Created|A new resource was created|Successful POST|
|**204** No Content|Success, nothing to return|Successful DELETE/PUT/POST without body|
|**400** Bad Request|Invalid request / data|Wrong JSON, missing field|
|**401** Unauthorized|Not authenticated|Missing/invalid token|
|**403** Forbidden|Authenticated but not allowed|User without the right role|
|**404** Not Found|Resource does not exist|GET /produits/9999|
|**500** Internal Server Error|Server crashed|Unhandled exception|

- Families: **2xx** = success, **3xx** = redirection, **4xx** = client error, **5xx** = server error.

# Web services

## Definition

**Web services** are IT services from the family of web technologies that allow **communication between heterogeneous applications in distributed environments**. They let applications call functionality **remotely** over the network, **independently of their platform and programming language**.

# Rest

**REST = REpresentational State Transfer.** Defined in the PhD thesis of **Roy Fielding in 2000**.

- It is not tied only to the web: it **can use protocols other than HTTP** (but in practice it is almost always HTTP).
- Used to build **resource-oriented applications (ROA)** or **data-oriented applications (DOA)**.
- Applications that respect the REST architecture are called **RESTful**.

"Is REST a protocol?" -> **NO**: it is an **architectural style**. This is a classic True/False trap.

 
|**REST IS...**|**REST IS NOT...**|
|---|---|
|An **architectural style** (an architecture system)|A protocol|
|An **approach to build an application**|A format|
|Inspired by the architecture of the web, strongly based on **HTTP**|A standard|


**Note**:

What happens if we **read with POST**, **update with DELETE**, or **delete with PUT**?

- REST **does not forbid** it technically (it still "works").
- But then your application **does not respect REST requirements** and is therefore **not RESTful**.

## advantages and disadvantages
 
| **Advantages**                              | **Disadvantages**                                                                     |
| ------------------------------------------- | ------------------------------------------------------------------------------------- |
| **Simplicity** of implementation            | **Restricted security** (relies on HTTP methods/HTTPS, no built-in security standard) |
| **Human-readable** messages (JSON)          | No strict **formal contract** (informal schema; WADL/OpenAPI optional)                |
| **Scalability / evolvability** (stateless)  |                                                                                       |
| Based on the **principles of the web**      | Many endpoints to maintain; versioning needed (/v1, /v2)                              |
| **Multiple representations** (XML, JSON...) | Not ideal for complex, flexible queries                                               |
| Light messages, good performance            |                                                                                       |
## Charateristics

- **Stateless:** each request sent to the server must contain **all the information related to its state** and is processed **independently of all other requests**. Result: **minimised system resources** (no session management, no state kept).
- **Uniform interface** based on HTTP methods (**GET, POST, PUT, DELETE**).
- **Resource-based:** RESTful architectures are built from resources **uniquely identified by URIs(Uniform resource indentifier)**.

## Rest components

  
|**Block**|**Meaning**|**Example**|
|---|---|---|
|**Resource**|An identifiable object of the system, identified by a **URI**|http://unice.fr/cursus/master/miage|
|**Verb (method)**|The HTTP method that manipulates the resource|GET, POST, PUT, DELETE|
|**Representation**|A view of the state of the resource: the data format exchanged|JSON, XML, text/plain|

A resource is any identifiable entity, object, or piece of data (such as a webpage, an image, a file, a user profile, or an abstract concept), while a URI (Uniform Resource Identifier) is the string of characters used to uniquely identify that resource.

##  Representation

A **representation** is the data exchanged between client and server for a resource. With **GET**, the server sends the **state** of the resource to the client. With **PUT/POST**, the client sends the **state** of a resource to the server. Possible formats: **JSON, XML, XHTML, CSV, text/plain...**

|**Header**|**Who sends it**|**Meaning**|**Everyday comparison**|
|---|---|---|---|
|**Accept**|Client|The format I want to receive (e.g. XML or JSON)|Ordering the menu **in French**|
|**Content-Type**|Whoever sends a body|The format of what is inside this message|The **label on a parcel** saying what is inside|


Example: a client sends "GET /users/1" with Accept = XML. The server replies "200 OK" with Content-Type = XML and the user's data written in XML.


## WADL

- **WADL = Web Application Description Language**, a **W3C standard**.
- Describes the elements of a service: **resource, method, parameter, response**.
- Allows **dynamic interaction** with REST applications.

## JSON

**JSON** is a data-exchange format, **easy to read for humans and to parse for machines**. Based on JavaScript but **independent of programming languages** (C, C++, Perl, Python, Java, C#, VB, JavaScript...). It has **two structures**:

- A collection of **key/value pairs** -> **Object** { }
- An **ordered list** of values -> **Array** [ ]

# Distributed system

**Definition:** a **network of independent computers that collaborate to reach a common goal, appearing to users as a single, coherent system**. They share resources, handle tasks collaboratively and are often spread over several sites.

  
|**Characteristic**|**Meaning**|**Example**|
|---|---|---|
|**Decentralisation**|Resources and processes are spread over several **nodes**|Orders on server A, payments on server B|
|**Transparency**|The distributed nature is **hidden** from users: one unified interface|You use amazon.com without knowing which server answers|
|**Scalability (Évolutivité)**|The system grows by **adding nodes** without major reconfiguration|Add 2 more servers on Black Friday|
|**Fault tolerance**|Designed to **handle and recover from failures** gracefully|One server crashes, another takes over|

![[image-448.png]]

## Asychrone communication

  
|**Synchronous**|**Asynchronous**|
|---|---|---|
|**Principle**|Service A opens a connection to service B (maybe on another machine) and **waits for the answer**|A sends a **message to a broker** (provider); the broker **delivers** it to B later|
|**If B is down**|**No communication** is possible - A is blocked/fails|A can still send: the message is **kept in the queue** until B reconnects|
|**Coupling**|Stronger (A depends on B being available)|Looser (A and B do not know each other)|
|**Technologies**|**RMI, CORBA, HTTP / REST**|**JMS, AMQP, STOMP, MQTT**; brokers: **RabbitMQ, ActiveMQ, HornetQ, Kafka**|
|**Use when**|You need the answer immediately (get a price, check login)|Notifications, order processing, long tasks, events|

![[image-449.png]]

## Composition in distributed system

**Composition** is the method of integrating several **distinct services, modules or components** into **one coherent system**. It lets you build complex applications by combining parts that were **developed independently**. It guarantees:

 
|**Benefit**|**Meaning**|
|---|---|
|**Scalability (Évolutivité)**|Evolve by adding/adjusting single components without redesigning the whole architecture|
|**Flexibility**|Easy integration, replacement or dynamic update of components; adapts to new technologies|
|**Maintainability**|Smaller components developed independently: simpler tests, debugging and maintenance|
|**Reuse and efficiency**|Reuse existing components/services - less redundancy and development effort|
|**Fault tolerance and reliability**|A failure is isolated in one component; the others keep working|

### of composition

  
|**Vertical (by layers)**|**Horizontal (by services)**|
|---|---|---|
|**Idea**|Each service is organised in **layers** (presentation, business, data); each layer can be deployed on a different node|Each service is an **autonomous microservice** specialised in one function, with **its own layers** (UI, business, data)|
|**Example**|Server 1, 2, 3 each = UI + business + data|User service + Order service + Payment service, each with its own database|
|**Communication**|Between layers|Between services through **APIs (REST, gRPC...)**|
|**Advantages**|Coherence, simple management, easy to understand and maintain|High flexibility and scalability, independent deployment, better load distribution and resilience|
|**Drawbacks**|Less flexible: hard to evolve one layer alone; possible **duplication** of code and resources|More complexity (communication between services); **distributed transactions** harder|

![[image-450.png]]

### Techniques




### Architecture patterns

 
|**Pattern**|**Idea**|
|---|---|
|**Microservices architecture**|Application split into small independent services, each with one function; communicate via APIs; scale and update independently|
|**SOA**|Services provide business functions and interact via standardised protocols; stresses **reuse and interoperability**|
|**Event-driven architecture (EDA)**|Events trigger actions; asynchronous communication; better reactivity and scalability|
|**Layered architecture**|Layers (presentation, business logic, data access): separation of concerns, modularity|
|**Broker pattern**|A central broker/middleware manages communication and coordination: loose coupling|
|**API gateway pattern**|Single entry point to several backend services; handles routing, authentication and other cross-cutting concerns|
|**CQRS**|Command Query Responsibility Segregation: separate **commands (writes)** from **queries (reads)** so each can be optimised and scaled independently|

### advantages and disadvantages

  
|**Challenge**|**Problem**|**Solution**|
|---|---|---|
|**Managing complexity**|Interactions between many services are complex|Modular design, good documentation, a **service registry**|
|**Data consistency**|Hard to keep data consistent across services|**Eventual consistency**, **distributed transactions**, efficient conflict handling|
|**Fault tolerance and reliability**|Failures impact global reliability|**Redundancy**, **retry** mechanisms, robust **monitoring and alerting**|
|**Performance and latency**|Communication between services adds latency|**Caching**, **load balancing**, optimised communication|
|**Security**|Securing several levels is complex|**Encrypt** data, strong **authentication and authorisation**, secure the **APIs**|

### Middleware and frameworks

   
|**Middleware**|**Type of communication**|**Examples**|**Role**|
|---|---|---|---|
|**Message brokers**|Asynchronous|RabbitMQ, Apache Kafka, ActiveMQ|Message queues, routing and delivery; decouple services; event-driven architecture|
|**API gateways**|Single entry point|Kong, NGINX, AWS API Gateway|Routing and authentication, rate limiting, response aggregation; simplify client access|
|**Service meshes**|Internal communication|Istio, Linkerd, Consul Connect|Traffic routing, load balancing, security and observability between microservices|
|**Enterprise Service Bus (ESB)**|Centralised integration|MuleSoft, WSO2, IBM Integration Bus|Integrate heterogeneous applications; mediation and transformation of exchanges; coordinate complex business processes|
![[image-451.png]]

# Microservice

## Monotholic approach

A **monolithic application** is developed as **one single block** (**war, jar, ear, dll**), with **one technology**, and deployed **in one application server**. All layers (web, business, DAO, technical services) live in the same package.

![[image-452.png]]

### Drawbacks

- It **centralises all functional needs** in one block.
- Everything is built with **one single technology**.
- **Each modification** requires: **re-testing for regressions** and **redeploying the whole application**
- **Difficult to evolve** functionally.
- **Delivery in one block** ("big bang"): the client waits a long time before seeing the first versions.

## Microservice approach

**Microservices** are an architecture and development approach where an **application is composed of small services**. The idea: **split a big problem into small units**, each implemented as a microservice.

### Charateristics

- Each service is responsible for **one functionality**.
- Each microservice is **developed, tested and deployed separately** from the others.
- Each can use a **different technology** (Java, C++, C#, PHP, NodeJS, Python...).
- Each service runs in **its own process**.
- They use **lightweight communication mechanisms (REST)**.
- The only relationship between them is **data exchange through the APIs they expose** (REST, messaging JMS/AMQP...).
- Combined, they can perform **very complex operations**.

### Advantages

- **Loosely coupled** - each microservice is physically separated from the others.
- **Relative independence of teams** that develop the different microservices.
- Easy **testing** and **deployment**; **continuous delivery**.
- Fits well with software-engineering processes: **TDD (Test-Driven Development)** and **agile methods**.

### Components

ike a monolith, a microservice can be made of **very small layers**: a **DAO layer**, a **business layer** and **technical layers** (REST, JMS, AMQP, security...). It owns its **data**.

![[image-453.png]]