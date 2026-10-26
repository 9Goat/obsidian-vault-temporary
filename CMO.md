# Software

software is omni present, it is everywhere in our lifes, which makes us depend on it for everyday tasks

## Benefits

- it speeds up processing of  complicated tasks
- it never gets tired
- has a high capacity and calculation speed
- it allows us to communicate freely with others

## Drawbacks

- a single failure, bug  or error can lead to catastrophic disasters (in the slide she talks about disasters)
- for critical domains like medicine the code quality must be verified to insure the safety of others 

## Definition of software

software is an information transformer: **a software is a set of information relating to processing carried out automatically by a computer tool.**

in french:

- Un logiciel est un ensemble d'informations relatives à des traitements effectués automatiquement par un outil informatique.


    - Une forme exécutable:  séquence d'instructions exécutables par une machine
     - Une forme non exécutable: documentation (développement, installation, utilisation et maintenance), Des données.

## Software categories

  
|**Category**|**Definition**|**Examples**|
|---|---|---|
|**Generic software**|Stand-alone systems sold to the general public (system and basic software)|Windows, Linux, an office suite, a web browser|
|**Custom software**|Stand-alone systems developed for the needs of one client (applications)|A hospital’s patient-management system, a bank’s internal accounting application|


![[image-430.png]]


## Software projects

   
|**Category**|**Team**|**Duration**|**Size (lines of code)**|
|---|---|---|---|
|**Trivial**|1 programmer|1–4 weeks|< 500|
|**Small**|1 programmer|1–6 months|1,000–2,000|
|**Medium**|2–5 programmers|1–2 years|5,000–50,000|
|**Large**|5–20 programmers|2–3 years|50,000–100,000|
|**Very large**|100–1,000 programmers|4–5 years|about 1 million|
|**Extremely large**|2,000–5,000 programmers|5–10 years|1–10 million|

Large software is not just “small software, but bigger”. It is qualitatively different:

- It is **complex**: many thousands of lines of code spread over several units.
- It is **developed by several people**, which creates problems of communication and coordination.
- **No single person can understand the whole design.** Modifying it therefore becomes difficult, and people must rely on the documentation.
- **Starting again from scratch is not an option**: the investment is too large.


Building a complex physical object requires drawings and plans; building large software is no different, so it cannot be done without a **specification** of its characteristics. But software has special properties that make it harder to manage than most physical products:

|**Aspect**|**Physical product**|**Software**|
|---|---|---|
|**Visibility**|Visible during construction|Impalpable; becomes visible very late|
|**Nature**|Manufacturing effort|Intellectual creation|
|**Ageing**|Wears out through use|Does not wear out, but **deteriorates** through successive changes|
|**Changes**|Usually local and predictable|Neither continuous nor localised: a minor change can have huge implications|

## Software quality

2 types:
- external: noticeable by users
- internal: concerns the developer (readable code, clean structure, good documentation)
	- Good internal quality usually leads to good external quality over time.

### factors that make software quality

  
| **Factor**          | **Meaning**                               | **Example**                                                         |
| ------------------- | ----------------------------------------- | ------------------------------------------------------------------- |
| **Compliance**      | Meets the user’s needs                    | The invoicing app computes taxes exactly as the accountant requires |
| **Reliability**     | Does not fail more than is allowed        | A banking server that stays up during peak hours                    |
| **Efficiency**      | Does not waste resources                  | A mobile app that does not drain the battery                        |
| **Maintainability** | Can evolve to follow changing user needs  | Adding a new payment method without rewriting the system            |
| **Usability**       | Friendly interface and good documentation | A new employee can use it after a short guide                       |

The importance of these quality factors will vary depending on the nature of the development project.

# Software development

## Definition

**Software development is the transformation of an explicitly expressed need into a working software.** The idea comes from a **client** (the user) and is developed by a **supplier**.

![[image-431.png]]

## good software

![[image-432.png]]


 
|**Client’s point of view**|**Supplier’s point of view**|
|---|---|
|Inexpensive|Minimise cost|
|Delivered on time|Minimise delays|
|Good quality|Meets the objectives that were fixed|
|Does exactly what is wanted|Maximise profit|

**requirements of a software project**

- **A development team.** It is not only programmers: project managers, testers, functional analysts and other roles take part.
- **Development tools:** compilers, editors, test environments, and so on.
- **Communication.** It is essential in every development project.

**Software industrialisation** 

Software development is becoming industrialised. The pressures behind this trend are:

- Projects are **more and more ambitious**.
- **Deadline pressure** is stronger.
- Expected **quality** is higher.
- **Offshoring** (work shared among teams in different countries), which makes communication even more important.

# Software crisis

## Symptoms of a software crisis

 
| **Symptom**     | **Description**                                         |
| --------------- | ------------------------------------------------------- |
| **Inadequacy**  | The delivered software does not match what users needed |
| **Delays**      | Software is often delivered late                        |
| **Costs**       | The planned budget is exceeded                          |
| **Reliability** | Software often breaks down                              |
| **Maintenance** | Complex and expensive                                   |

## Surveys

- survey showed that only 2% of software was used as delivered (reason? misunderstanding)
	- ![[image-433.png]]
- surveys also show that software barely gets delivered on time and at most of the times it exceeds the project budget(this happens when we try to guess instead of estimating)
	- ![[image-434.png]]
- another survey alot of software suffers from code quality (**30 and 85 errors per thousand instructions**.)
- Maintenance (fixing errors, adapting to change) consumes **40% to 75% of the global budget** of a software. Worse, the cost of a modification grows sharply the later it is made.
	- ![[image-435.png]]
	- why does this happen?: A misunderstanding corrected during the _definition_ phase costs 1 unit. The same misunderstanding discovered after installation can cost 60 to 100 times more. This is the economic argument for specifying carefully, testing early and, later, for agile feedback loops.

## causes of the crisis

1. **The science and technology were too young(Science, technologie trop jeune).** Software engineering had no mature methods yet.
2. **Inherent complexity:(Complexité inhérente)** too many communication links between people, too many interrelations between modules, systems too large to be grasped by one person, too many modifications, and extrapolations (“scaling up” from small projects) that are hard to make.

# Software engineering

Software engineering (**Génie Logiciel, GL**) was born in Europe,It was created to respond to the problems of software development described in the previous chapter.

- **involves problem solving**;
- **involves acquiring knowledge**;
- is **driven by motivations and reasons** (rationale);
- **applies the principles of engineering**.

It is composed of **methods, techniques and tools**, and goes beyond the mere activity of programming.

## Definition

The set of methods, techniques and tools contributing to the production of software, beyond the sole programming activity.

## Objectives

Software engineering is **the application of engineering principles to software development**. It establishes and applies **methodical and measurable approaches** to develop and maintain software, with the goal of obtaining systems that are **economical, reliable and efficient** in real operating conditions.

The three variables it tries to balance are **quality, cost and time (deadline)**. It also aims to **improve productivity** and **improve quality**, starting from needs and ending with the software, supported by tools, standards, methods and techniques.

![[image-436.png]]

![[image-437.png]]


## Requirements of software enginering

  
| **Principle**       | A general law governing a set of phenomena, verified by the correctness of its consequences | “Separate concerns”, “divide and conquer” |
| ------------------- | ------------------------------------------------------------------------------------------- | ----------------------------------------- |
| **Rule**            | A prescription imposed on someone in a given case                                           | “Every function must be documented”       |
| **Technique**       | What relates to practice and know-how in an activity                                        | Writing unit tests                        |
| **Method**          | A logically ordered set of steps leading to a result                                        | Waterfall method, Scrum                   |
| **Standard (norm)** | A rule fixing the type of a manufactured object and its manufacturing conditions            | ISO quality standards                     |
| **Methodology**     | Groups and applies methods and techniques                                                   | A company’s full development methodology  |
| **Tool**            | Supports the methodology                                                                    | Compiler, version-control system          |

![[image-438.png]]

![[image-440.png]]![[image-439.png]]


## Actors

Key element: **communication**. One person can play several roles, and several people can share the same role.
 
|**Role**|**Responsibility**|
|---|---|
|**Client / sponsor**|Pays for the system and defines the business goals|
|**User**|Uses the system daily; source of real needs|
|**Project manager (development manager)**|Plans, coordinates and tracks the project|
|**Solution architect**|Designs the overall structure of the system|
|**Infrastructure architect**|Designs servers, networks and deployment environments|
|**Developer / computer engineer**|Writes and integrates the code|
|**Tester**|Verifies that the software works and meets requirements|

# Agility

Agility is a **perpetual search for balance** between:

- **An active dimension:** doing, and proving that we know how to do.
- **A reactive dimension:** being opportunistic in the face of observed changes, in order to retain customers.
- **A proactive dimension:** creating value.

## Definition

An agile method is an **iterative and incremental** approach, run in a **collaborative spirit** with just enough formalism. It produces a high-quality product while taking into account changing customer needs.

**Iterative and incremental**:

- **Iterative** means repeating a cycle of work (plan, build, check) several times, improving each time.
- **Incremental** means delivering the product in usable pieces rather than all at once.

## agility is organized into


![[image-441.png]]


## Agile values

  
|**We value more…**|…**than**|**What it means in practice**|
|---|---|---|
|**Individuals and interactions**|processes and tools|Talking to people solves more problems than following a tool-driven process|
|**Working software**|comprehensive documentation|The best proof of progress is a product that runs; keep only documents that help|
|**Customer collaboration**|contract negotiation|Work with the customer throughout instead of arguing over contract clauses|
|**Responding to change**|following a plan|A plan is a guide, not a prison; adapt when reality changes|

## Twelves principals

12 princpals divided into 4 axes

![[image-442.png]]



### Axis 1 client statisfaction

- **Highest priority:** satisfy the customer by delivering regularly **features of high added value**. Focus on features with the most business value.
- **Welcome change**, even late. Agile processes harness change to give the customer a competitive advantage. _Commit only to what is clear and estimable._
- **Deliver working software frequently**, in cycles of a few weeks to a few months, with a preference for the shortest. _Work sequentially, not in parallel._

### Axis 2 individuals

- **Daily collaboration** between users (or their representatives) and developers throughout the project; encourage collaboration among all stakeholders.
- **Face-to-face dialogue** is the simplest and most effective way of passing information to and within the team. Discussing around a whiteboard is the best means of communication.
- **Motivated people:** give them the environment and support they need, and trust them. People do their best. _Prefer trust to control._
- **Self-organising teams** produce the best architectures, specifications and designs. People are more productive when they manage themselves: they take commitments they made themselves more seriously than commitments made for them.
- **Sustainable pace:** sponsors, developers and users should be able to maintain a constant rhythm indefinitely. Under pressure to work harder, people automatically reduce the quality of their work.

### Axis 3 excellent techniques

- **Working software is the main measure of progress.** A working product is a quality product. Seek quality _assurance_ throughout the project rather than quality _control_ just before delivery.
- **Continuous attention to technical excellence and good design** strengthens agility and satisfies customers by improving product quality.
- **Simplicity**, the art of minimising unnecessary work, improves both lead times and product quality.

### Axis 4: Continuous improvement

At regular intervals the team reflects on how to become more effective, then adjusts its behaviour accordingly. In practice: **check continuously how we work**, and **improve wherever we see room for improvement**

we do that by asking ourselves questions like:

- what went well
- what could we have improved
- what actions will we take to avoid making such mistakes

this is represented in  La  roue de Deming:

  
|**Step**|**Meaning**|**Example (a team after each iteration)**|
|---|---|---|
|**Plan**|Prepare and plan what will be done|Decide to reduce bug-fixing time next iteration|
|**Do**|Develop and implement|Introduce automatic tests for new code|
|**Check**|Control and verify results|Compare bug counts before and after|
|**Act (Adjust)**|Act, adjust, react|Keep the practice or change it, then start a new cycle|

![[image-443.png]]


### Summary

| **Axis**                   | **Principle (paraphrased)**                                                                     |
| -------------------------- | ----------------------------------------------------------------------------------------------- |
| **Customer satisfaction**  | 1. Satisfy the customer through rapid and continuous delivery of valuable features.             |
|                            | 2. Welcome changing requirements, even late in the project.                                     |
|                            | 3. Deliver working software frequently (every few weeks to few months, preferring the shorter). |
| **Individuals**            | 4. Business people and developers work together daily.                                          |
|                            | 5. Build projects around motivated individuals; give them support and trust.                    |
|                            | 6. Face-to-face conversation is the most efficient way to convey information.                   |
|                            | 8. Keep a sustainable pace that can be maintained indefinitely.                                 |
|                            | 11. The best architectures and designs emerge from self-organising teams.                       |
| **Technical excellence**   | 7. Working software is the primary measure of progress.                                         |
|                            | 9. Continuous attention to technical excellence and good design enhances agility.               |
|                            | 10. Simplicity (the art of maximising the work not done) is essential.                          |
| **Continuous improvement** | 12. At regular intervals, the team reflects on how to become more effective and adjusts.        |


