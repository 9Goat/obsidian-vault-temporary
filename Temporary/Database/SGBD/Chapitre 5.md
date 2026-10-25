# Profile management

## Definition 

A profile is a group of parameters that condition the environment in which a user will work. These parameters are divided into two main categories:

- **System Parameters:** These limit the user's rights regarding system resources, such as CPU or session limits.
- **Password Parameters:** These consist of clauses designed to secure user passwords.

## Creation and parameters

![[image-373.png]]

A profile is created using the `CREATE PROFILE` command followed by specific `LIMIT` clauses. Key parameters include:

- **Security Controls:**
    - `FAILED_LOGIN_ATTEMPTS`: Locks the account after a specified number of failed login attempts.
    - `PASSWORD_LOCK_TIME`: Sets the duration for which a password is valid.
    - `PASSWORD_GRACE_TIME`: The time allowed for a user to change their password once it has expired.
    - `PASSWORD_REUSE_MAX`: The time during which a user is prohibited from reusing a previous password.
- **Resource Limits:**
    - `CPU_PER_SESSION`: Defines the CPU work time allocated to a user.
    - `SESSION_PER_USER`: Limits the number of concurrent sessions a user can open.
    - `CONNECT_TIME`: The total time a user is permitted to stay connected to the database instance.
    - `IDLE_TIME`: The amount of allowed inactivity before a user is forcibly disconnected.
    - `LOGICAL_READS_PER_SESSION`: The total number of memory or disk reads allowed per session.

## Profile Administration

Once defined, profiles must be assigned and maintained:

- **Assignment:** You assign a profile to a specific user with the command: `Grant [nom du profil] to [utilisateur]`.
- **Modification:** Existing profiles can be updated using the `ALTER PROFILE [nom du profil] LIMIT [CLAUSE] [VALEUR DE LA CLAUSE]` command followed by the parameter and the new value.
- **Monitoring:** To view information regarding all existing profiles in the database, you can query the data dictionary view: `SELECT * FROM dba_profiles;`.

# Privileges

A privilege is defined as the right to execute a specific SQL command. This can include accessing a table, performing a database operation, or simply connecting to the database. Privileges can be assigned to individual users, all users simultaneously, or to specific roles.

here are two primary types of privileges:

- **System Privileges:** These allow users to perform broad administrative or development tasks across the database.
- **Object Privileges:** These grant the right to perform specific operations on a particular database object, such as a table or a view.

## System Privileges

There are approximately 127 system privileges, generally grouped by category. Examples include:

- **System Operations:** `create tablespace` (creating storage areas), `create database`, and `alter system` (modifying database parameters).
- **Schema Object Management:** `create table`, `create user`, and `alter profile`.

## Object Privileges

![[image-374.png]]

These privileges are specific to objects like tables, views, sequences, or procedures. Common object privileges include:

- **SELECT**: Right to view data in an object.
- **INSERT**: Right to add new data to a table.
- **UPDATE**: Right to modify existing data.
- **EXECUTE**: Specific to procedures, allowing the user to run the code.
- **INDEX**: Right to create an index on a table.

## Privilege Management (Grant and Revoke)

Privileges are managed using two main SQL commands:

### Grant

Used to assign rights. The `GRANT` command is used to **assign rights** to perform specific actions within the database.

**Syntax:** `GRANT [DBA/PRIVILEGE] ON [OBJET] TO [ROLE/UTILISATEUR/PUBLIC] WITH GRANT OPTION`

**Parameters:**

- **DBA:** Grants **all available privileges**.
- **PRIVILEGE:** Specifies the **particular privilege** to be assigned, such as `SELECT`, `INSERT`, `UPDATE`, or `EXECUTE`.
- **OBJET:** Defines the **database object** (e.g., a table, view, sequence, or procedure) on which the privilege is being granted.
- **ROLE:** The name of a **role** (a group of privileges) that will receive the new privilege.
- **UTILISATEUR:** The specific **user** to whom the privilege is being granted.
- **PUBLIC:** Assigns the privilege to **every user** in the database.
- **WITH GRANT OPTION:** A special clause that allows the recipient to **further grant** that same privilege to other users or roles.

### Revoke

The `REVOKE` command is used to **take away** previously granted privileges. The source notes that its syntax is identical to the `GRANT` command, except it uses `FROM` instead of `TO`.

**Syntax:** `REVOKE [DBA/PRIVILEGE] ON [OBJET] FROM [ROLE/UTILISATEUR/PUBLIC]`

**Parameters:**

- **DBA/PRIVILEGE:** Specifies which **set of rights or specific right** is being removed.
- **OBJET:** The **specific object** from which the rights are being retracted.
- **ROLE/UTILISATEUR/PUBLIC:** Identifies the **role, specific user, or the general public** from whom the privilege is being revoked.

# Roles

![[image-375.png]]

A role is a **grouping of privileges or even other roles**. Instead of manually assigning every single privilege to every user—which would be tedious and error-prone—an administrator can create a role, assign a set of privileges to it once, and then **assign the entire role to one or more users**. Users then automatically possess every privilege contained within that role.

## Creation of roles

To create a new role, use the **CREATE ROLE** command with the following syntax options: `CREATE ROLE [NOM DU ROLE] [NOT IDENTIFIED] [IDENTIFIED BY PASSWORD/EXTERNALLY]`.

- **NOT IDENTIFIED**: No authentication is required for a user to access the role.
- **IDENTIFIED BY PASSWORD**: A specific password is required to activate the role.
- **IDENTIFIED EXTERNALLY**: Access to the role is managed by an external source, such as the operating system.

## Managing roles

The system uses the same **GRANT** and **REVOKE** logic seen in the previous section to handle roles:

- **Assigning a role to a user:** `GRANT [NOM DU ROLE] TO [UTILISATEUR/ROLE/PUBLIC]`.
- **Assigning a privilege to a role:** `GRANT [NOM DU PRIVILEGE] ON [NOM DE L'OBJET] TO [NOM DU ROLE]`.
- **Removing a role:** Use the **REVOKE** command to take a role away from a user.
- **Auditing:** To see all roles existing in the database, query the data dictionary: `SELECT role FROM dba_roles;`.

**Predefined Roles**

![[image-376.png]]

Oracle provides several standard predefined roles to handle common tasks:

- **CONNECT**: Grants the basic right to create a session (`CREATE SESSION`).
- **RESOURCE**: Provides a suite of rights for developers, including creating tables, sequences, procedures, and types.
- **DBA**: Contains nearly all system privileges and should **only** be granted to actual database administrators.
- **SELECT_CATALOG_ROLE**: Grants access to over 1,700 object privileges specifically on the data dictionary.
- **SCHEDULER_ADMIN**: Allows users to manage database jobs and the system scheduler.

# Users

## Creating users

The `CREATE USER` command is used in Oracle 10g to create a new database account and define its specific operating environment

```SQL
CREATE USER [NOM D'UTILISATEUR] IDENTIFIED BY [MOT DE PASSE]/EXTERNALLY DEFAULT TABLESPACE [tablespace] TEMPORARY TABLESPACE [tablespace] QUOTA [TAILLE M] on [tablespace] QUOTA [TAILLE M] on [tablespace] PASSWORD EXPIRE PROFILE [nom du profil] ACCOUNT [LOCK/UNLOCK]
```

- **[NOM D'UTILISATEUR]**: Specifies the name of the user account being created.
- **IDENTIFIED BY [MOT DE PASSE]**: Sets a database password that the user must provide to connect.
- **EXTERNALLY**: Instead of a database password, this indicates that the user is identified by the **operating system** (external identification).
- **DEFAULT TABLESPACE [tablespace]**: Defines the primary storage area (tablespace) where all data segments created by this user will be stored.
- **TEMPORARY TABLESPACE [tablespace]**: Specifies the location where the server allocates temporary space ("extents") for disk write operations, such as sorting, during a session.
- **QUOTA [TAILLE M] on [tablespace]**: Sets a physical limit on the amount of space (e.g., in Megabytes) the user is allowed to consume within a specific tablespace.
- **PASSWORD EXPIRE**: A security feature that forces the user to **immediately change their password** the first time they log in to the database.
- **PROFILE [nom du profil]**: Assigns a predefined profile to the user, which regulates their system resource usage and password security rules.
- **ACCOUNT [LOCK/UNLOCK]**: Determines the initial status of the account. **LOCK** disables the account so it cannot be used, while **UNLOCK** allows the user to connect immediately.

## Managing users

- **Modification:** If a user's requirements change, the **ALTER USER [name] [parameters to modify]** command is used to update any of the parameters defined during creation.
- **Deletion:** To remove a user from the system, the command **DROP USER [nom d'utilisateur] CASCADE** is employed, where the `CASCADE` clause ensures all objects owned by that user are also removed.

## Meta data

to access informations about the user we must access it via the `dba_users` with this command 
` SELECT [information(s) desirée] FROM dba_users;`

**Here is a list of meta data information we can get from this command** 

![[image-377.png]]