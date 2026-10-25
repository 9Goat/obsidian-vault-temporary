# Database
## Data base definition

A database is defined by 3 key characteristics:

- **Collection of Data:** It is a gathered set of information that is "inter-related," meaning the pieces of data have logical connections to one another.
- **Physical Storage:** This data isn't just floating around; it is recorded on a **physical support** (like a hard drive or server).
- **Simultaneous Access:** One of the most important features is that it can be accessed by **multiple users at the same time**.

**Short definition**: a database is defined as a **collection of related data, stored on a physical support, and accessible at the same time by several users**

## The 3-Level ANSI/SPARC Architecture

According to the **ANSI/SPARC** standard, a database is described at three distinct levels. This separation allows different people (users, developers, and administrators) to look at the same data in different ways.

1. **Conceptual level**:
	 - It describes the **real-world universe** using entities, their attributes, and relationships between them.​
	- At this level, we **ignore physical storage** and specific user views: we only care about the global logical structure (global logical schema).
	Example: for a university:
	- Entities: Student, Course, Enrollment
	- Attributes: Student(id, name), Course(code, title), Enrollment(grade, date)
	- Relationships: Student is enrolled in Course.
2.  **Internal level** :
	- It describes exactly how the data is stored in the computer's memory (secondary storage) and how the logical structures are mapped to physical ones.
	- It shows the **mapping** between logical structures (tables, relationships) and **physical structures** (files, indexes, blocks).
	 **Example** (university database):  
	- Conceptual: "Student(id, name)"  
	- Internal: "Student table stored in file students.dat, using B-tree index on id column, records of 128 bytes each"
3. **External level:
	- -It corresponds to the **different views that users or applications have** on the conceptual schema.
	- Each external schema shows **only part of the data**, in a form adapted to a category of users (for example, a “Student view” that shows only some columns and some tables).
	- For example, a student might see their grades, while a professor sees the whole class list. Each user only sees the part of the database that is relevant to them.

## The Professionals Around a Database

### Database Administrator (DBA)

person in charge of the technical control of the system

**Main tasks**:​

- Define the **conceptual schema** (logical structure)
- Define the **internal schema** (physical storage)
- Link users to their **external views**
- Ensure **security and integrity** (data is safe and correct)
- Set up **backup and recovery** procedures
- Monitor **performance** and adapt to new needs

### Tool Expert

A **specialist** who knows many tools and technologies used around complex database environments.​ They help the team choose and use the right tools to work efficiently.

**Main tasks**:

- Master technologies and methodologies to improve the database environment
- Train and support the database team on these tools
- Stay up to date with new developments (reporting, data analysis, data preparation, etc.)
- Create documentation that helps the database team

### Application Developer

Builds the **applications** that use the database (web apps, desktop apps, reports, etc.).

**Main tasks**:​

- Analyze and specify user needs in terms of applications
- Develop apps that access and use the database correctly
- Improve and maintain existing applications
- Find and fix programming problems
- Document changes and suggest improvements

### Network and Infrastructure Specialist

Takes care of the **servers and network** where the DBMS and applications run.

- Install, configure, and maintain servers and network equipment
- Manage operating systems and related software
- Define and manage network topology and security (access rights, group policies, etc.)
- Ensure the network works well and is performant
- Troubleshoot hardware and software problems on the network

So if the database server is down or unreachable because of network issues, this specialist is the one who fixes it.

## end user

Anyone who **uses the data** through applications or tools (students, employees, customers, etc.).​  
They don’t manage the database; they just **consume** the information.


| Role                       | Main focus                                    |
| -------------------------- | --------------------------------------------- |
| DBA                        | Structure, security, integrity, backups, perf |
| Expert en Outils           | Tools and technologies around the DB          |
| Développeur d’applications | Applications that use the DB                  |
| Spécialiste réseau         | Servers, OS, network, connectivity            |
| Utilisateur final          | Uses data via applications                    |


# SGBD

## Definition

A **SGBD** (Système de Gestion de Base de Données) is a **software system that manages a database**.  It lets you **store, organize, access, modify, and secure data** in a consistent way, instead of manipulating raw files directly.

### What is an SGBDR?

a SGBDR is a software system that manages a **relational database** and it can be of type **client/serveur** (Oracle, SQL Server, MySQL, PostgreSQL) or **fichiers partagés** (Access, etc.).

### Types of SGBDR

- **Client/serveur**
    - The database is on a **server**.
    - Clients (applications, users) connect over the network.
    - Used in professional environments (Oracle, SQL Server, MySQL, PostgreSQL).
- **Fichiers partagés**
    - The database is mainly a **file** shared on a network or local machine.
    - Used for smaller applications (Access, older systems like DBase, Paradox).

## Characteristics of a database

### Physical Independence

**What it means**: You can change **how data is stored physically** (files, disks, indexes) without affecting the **logical structure** (tables, relationships) that users see.

**Example**: DBA moves tables to SSD disks or changes file format → users and applications notice **nothing**.

### Logical Independence

**What it means**: You can change the **logical structure** (add tables, change relationships) without rewriting all user applications.

**Example**: DBA splits a "Customers" table into "Customers" + "VIP Customers" → external views stay the same for normal users.

### Manipulabilité

**What it means**: Even **non-technical users** can query data without knowing internal technical details (file names, indexes, etc.). They use a high-level language like **SQL**.

**Example**: A manager writes `SELECT name FROM students WHERE grade > 14` without knowing where the data is physically stored.

### Fast Access

The system uses smart algorithms to answer queries quickly.

### Administration centralisée

The **DBA** can centrally manage data insertion, updates, integrity checks, etc., instead of each user managing their own files. (One administrator can manage everything from one place - adding data, checking integrity, etc.)

### Reduced Redundancy

Avoids storing the same information multiple times, saving space and preventing errors.

**Example**: Instead of storing "John Doe, 123 Main St" in 10 different tables, store it once in "Addresses" table and reference it.

### Data Integrity

Data stays **consistent**: when A references B, B must exist (foreign key constraints, NOT NULL, etc.).

**Example**: You can't enroll a student in a course if the course ID doesn't exist.

### Sharability

It allows **multiple users** to access and work on the same data at the same times

### data security

The SGBD controls **who can see/modify what** (user rights, roles, encryption).

**Example**: Students see only their grades, teachers see their class grades, admin sees everything.


## SGBD components


###  DBMS Engine

This is the **central part** of the DBMS that talks to the operating system (Windows, Linux, etc.).  
It manages access to data files, moves data between disk and memory, and coordinates all other DBMS components.

### Data definition system

This part contains the tools to **define and modify the structure** of the database.  
It is used to create tables, relationships, constraints, users, etc. (in SQL, this corresponds to DDL commands like `CREATE TABLE`, `ALTER TABLE`, etc.).

### User interface

This is how **users and programs interact** with the DBMS.  
It can be:

- A **command-line** tool (like SQL*Plus, psql, etc.)
- A **graphical** tool (GUI) where you click to run queries, create tables, etc.  

Applications also connect through this interface using a query language like SQL or PSQL


### Application development tools

These are tools that help **build applications** on top of the database. They help create the visual parts of a database system, like graphical forms, custom menus, and generated reports.

### Data administration system

This is a set of **utilities** for the DBA.  
It includes tools for:

- Backup and restore
- Performance tuning and optimization
- Storage management (space allocation, file management)

The DBA uses these tools to keep the database **safe, efficient, and available**.

### Data dictionary (metadata)

The data dictionary stores **metadata**: data about the data. It tracks the structure, how objects relate to each other, user privileges, and integrity rules.....

### Communication manager

This component manages the **communication between the DBMS and the outside world**.managing requests coming in from users, other applications, or even other database systems.

## Oracle tools

### Oracle Enterprise Manager (OEM)

**What it is**: A **graphical web-based administration tool** that you access through a browser. 

**Main use**: Central dashboard to monitor and manage your entire Oracle database environment.

**Key features**: Shows performance charts, alerts for problems, links to other tools, and lets you do most DBA tasks through a friendly interface instead of command line.

### Database Configuration Assistant (DBCA)

Think of this as an **installation wizard**. It is specifically used when you are first creating a new database

### Oracle Wallet Manager (OWM)

Tool to manage **secure connections** (SSL/TLS encryption) to the database.

### Network Configuration Assistant (NETCA)

**What it is**: **Wizard for network setup**.  

**Main use**: Configures how clients connect to the Oracle server over the network (listener configuration, service names, ports).

### Recovery Manager (RMAN)

It is the dedicated tool for performing backups and recovering data if something goes wrong.

### Database Upgrade Assistant (DBUA)

Used for **updates**. It helps migrate a database from an older version to a newer one.

### SQL* Plus

**What it is**: **Command-line SQL tool** (like a terminal).  

**Main use**: Run SQL queries, PL/SQL scripts, execute DBA commands. Very powerful for automation.

### EXPORT/IMPORT utilities

They allow you to move objects (like tables) out of the database into a file, or bring them back in

### Oracle environment

a command line tools that allows you to configure oracles environment variables

## Oracle Processes

A process is a **program in execution** - a connection to the operating system doing a specific task.
In Oracle, these processes start when the database starts and stay active the whole time.

There are two main types of processes you need to know:

1. **User processes: Each user/app that connects creates one**
   - They are responsible for running the application that connects the user to the database.
   - Communicates with Oracle server processes
2. **Oracle processes: Do the real database work**
   a) Server processes: Handle each user request
   b) Background processes: These work behind the scenes to keep the database healthy (like writing data to disks or managing error logs)

### Oracle application architecture

**Front-end**: Users + applications (what you see/interact with)  
**Back-end**: DBMS + actual database files (the engine)

![[image-283.png]]

![[image-284.png]]