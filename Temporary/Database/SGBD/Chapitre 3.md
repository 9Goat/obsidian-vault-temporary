# Introduction


In the world of databases, a **transaction** is defined as a single operation, or a sequence of operations, performed by a user or a program to **read or update** the contents of the database.

## types of transactions

- **Lecture-seule (Read-Only):** This transaction only uses the `Lire(X)` (Read) operation. It looks at data but never changes it.
- **Lecture-écriture (Read-Write):** This transaction uses both `Lire(X)` and `Écrire(X)` operations to modify data.

# Transaction operations

1. **Lire(X) (Read):** This involves finding the data (X) on the disk, loading it into memory, and assigning it to a variable so the program can use it.
2. **Écrire(X) (Write):** This takes a value from a variable in memory and saves it back onto the disk into the database object (X).

A transaction is not complete until it is "closed" by one of two specific commands:

- **Commit:** This **validates** the transaction, making all the changes permanent.
- **Rollback:** This **cancels** the transaction, undoing any changes made during that sequence so the database returns to its previous state.

## Transaction annotations

- Ti​ **:** Refers to a specific transaction (e.g., T1​, T2​).
- li​[x]**:** A **Read** operation (l for _lire_) of data item x performed by transaction i.
- ei​[x]**:** A **Write** operation (e for _écrire_) of data item x performed by transaction i.
- ci​ **:** A **Commit** operation, which marks the successful validation and permanent saving of transaction i.
- ri​ **:** A **Rollback** operation, which cancels transaction i and undoes any changes it made

# States of a transaction

![[image-364.png]]

- **Active:** This is the starting state.A transaction enters this state as soon as it begins and stays here while it is performing its **Lire(X)** and **Écrire(X)** operations.
- **Partially Committed:** The transaction moves here after its **very last operation** has been executed, but before the changes are permanently saved to the disk.
- **Committed:** Once the DBMS confirms that all changes are successfully and permanently written to the database, the transaction enters this state.
- **Failed:** If an error occurs (like a system crash, a logic error, or a violation of a rule) while the transaction is in the Active or Partially Committed state, it moves to "Failed".
- **Terminated:** This is the final state. Whether the transaction was successful (Committed) or had to be canceled (Aborted/Rolled back), it always ends here.

The DBMS  memorizes those specific states with the following commands:

- **BEGIN TRANSACTION:** This marks the start and moves the transaction into the **Active** state.
- **READ or WRITE:** These are the actual operations performed while the transaction is in the **Active** state.
- **END TRANSACTION:** This signals that the operations are finished, moving the transaction to the **Partially committed** state.
- **COMMIT:** This validates the changes and moves the transaction to the final **Committed** state.
- **ROLLBACK (or ABORT):** This cancels the transaction if an error occurs, moving it to the **Failed** state.
- **Undo**: This is similar to a rollback but it applies to a **single operation** rather than the entire transaction. It is used to remove changes from transactions that never reached a "Commit".
- **Redo**: This specifies that certain operations of a transaction must be **replayed**. 

# The ACID Properties


- **Atomicité (Atomicity):** Known as the **"all or nothing" rule**, it ensures that a transaction is either executed in its entirety or not at all.
    - **Example:** In a money transfer where $50 is subtracted from account X and added to account Y, if the system crashes after the subtraction but before the addition, **Atomicity** ensures the whole transaction is canceled (Rollback) so the money isn't lost.

- **Cohérence (Consistency):** This ensures the transaction takes the database from one **consistent state** to another, respecting all database integrity constraints (such as conditions like age>0).
    - **Example:** If a bank rule states that the sum 2 balances after a transaction must remain constant, a transaction that subtracts $50 from X and adds $50 to Y preserves **Consistency** because the total balance remains the same after the transaction.

- **Isolation:** ensures that even though many transactions are running at the same time, they should not interfere with each other.
    - **Example:** While transaction T1 is updating your balance, transaction T2 is prevented from reading that "in-progress" value. This prevents a **"dirty read,"** where T2 might see money that hasn't officially been committed yet.

- **Durability (Durabilité):** Once a transaction is **committed (validated)**, its effects are **permanent** and will survive even a system or power failure. This is typically done using a **Redo Log** (or journal), which serves as a history of all operations.
    - **Example:** After you receive a "Transfer Successful" message, the DBMS writes the update to a **Redo Log** on the disk. Even if the server loses power a minute later, your new balance remains saved.

# Errors with multiple transactions

## Lost update

A **Lost Update** happens when two transactions (T1 and T2) read the same data, modify it, and then both try to write it back. the second transaction's "Write" completely **overwrites** the first one's work, making it disappear.

### Example

1. **T1** reads the balance (500) and subtracts 200 in its local memory (New balance = 300).
2. **T2** reads the balance (still 500) and adds 90 in its local memory (New balance = 590).
3. **T1** writes its result (300) back to the database.
4. **T2** writes its result (590) back to the database.

**The result:** The final balance is **590**. The subtraction of 200 by T1 is completely lost! If the system worked correctly, the final balance should have been 390 (500 - 200 + 90).
![[image-365.png]]

## Inconsistent Analysis

An **Inconsistent Analysis** occurs when one transaction is trying to calculate a summary (like a total sum) while another transaction is changing values resulting in an inconsistent result. 

### Example

Imagine you have three accounts: **X = 500**, **Y = 200**, and a variable **Z** to store the total.

1. **Transaction T1** wants to calculate the sum of X and Y.
2. **Transaction T2** wants to transfer 100 from X to Y.

**The "Inconsistent" Timeline:**

- **T1** reads **X** (500) and adds it to its total **Z** (Z = 500).
- **T2** then subtracts 100 from **X** and writes it (**X is now 400**).
- **T2** adds 100 to **Y** and writes it (**Y is now 300**).
- **T1** now reads **Y**, but it reads the **new** value (**300**) and adds it to its total.
- **Final Result for T1:** Z = 500 + 300 = **800**.

In reality, the total should have been **700** (500+200). T1 got an incorrect result because it saw the "old" X but the "new" Y.
![[image-366.png]]

## Dirty read

A **Dirty Read** (or _Dépendance non validée_) happens when one transaction reads data that has been changed by another transaction, but **not yet committed**.

### Example

Imagine a bank account starting with a balance of **500**.

1. **T1** reads the balance: **Lire(Solde)** -> 500.
2. **T1** subtracts 100 and saves it: **Écrire(Solde)** -> 400.
3. **T2** comes along and reads the balance: **Lire(Solde)** -> **400**.
    - _This is the "Dirty Read." T2 is seeing a value that T1 hasn't officially finalized yet._
4. **T1** encounters an error and cancels everything: **Rollback**.
    - _Because of Atomicity, the balance is automatically set back to 500._
5. **T2**, unaware of the Rollback, continues its work. It subtracts 200 from the 400 it read earlier and saves it: **Écrire(Solde)** -> **200**.

**The result:** The final balance is **200**, but it should have been **300** (500 - 200). T2 used a "fake" intermediate value of 400 that was eventually deleted.
![[image-367.png]]

## Unrepeatable Read

An **Unrepeatable Read** occurs when a single transaction reads the same data item twice, but gets **two different values** each time.

### Example

Imagine a bank account starting with a balance of **500**.

1. **T1** reads the balance: **Lire(Solde)** -> 500.
2. **T1** performs some internal calculation (like calculating interest based on that 500).
3. **T2** suddenly starts, subtracts 200, and saves it: **Écrire(Solde)** followed by a **Commit**. The balance on the disk is now **300**.
4. **T1** reads the balance again for a final check: **Lire(Solde)** -> **300**.

**The problem:** Transaction T1 is now confused. It started its work thinking the balance was 500, but now it sees 300. Its calculations might no longer be correct because the "ground" shifted beneath its feet.

![[image-368.png]]

# Serial vs. Serializable Execution

There are two ways to run transactions:

- **Exécution en série (Serial Execution):** This is when transactions are executed one after another, in their entirety, without any overlap (e.g., T1 finishes completely, then T2 starts).
- **Exécution sérialisable (Serializable Execution):** When the DBMS mixes the operations of T1 and T2 together to go faster. By definition, an execution is "serializable" if it is **equivalent to some serial execution**.

The job of the database's **Scheduler (Ordonnanceur)** is to take a messy, interleaved execution and ensure it is "serializable"—meaning it behaves exactly as if the transactions had run one at a time.

# Conflicting Operations

To ensure an interleaved execution is serializable, the system looks for **conflicts**. Two operations from different transactions are in **conflict** if they access the **same data item** and at least one of them is an **Écrire (Write)**.

- **Commutable (Safe):** The order doesn't matter. The only pair of operations that is always commutable on the same data is **Lire-Lire (Read-Read)**. You and another user can both read the same bank balance at the same time without any issues.
- **Conflictuelle (Unsafe):** The order **does** matter. These include:
	1. **Different Transactions:** The operations must be performed by two different transactions (e.g., T1​ and T2​).
	2. **Same Data Item:** Both operations must access the exact same piece of data (like "Account X").
	3. **At least one Write:** This is the key part—for a conflict to exist, **at least one** of the operations must be an **Écrire (Write)**.

**The Three Types of Conflicts**

Based on those rules, there are actually three specific combinations that create a conflict:

- **Read-Write (Lire-Écrire):** T1​ reads data, then T2​ tries to change it.
- **Write-Read (Écrire-Lire):** T1​ changes data, then T2​ tries to read that change.
- **Write-Write (Écrire-Écrire):** Both T1​ and T2​ try to change the same data.

- A **Dirty Read** occurs when a transaction reads data that has been modified by another transaction but **not yet committed**.
- A **Non-Repeatable Read** happens when a transaction reads the same piece of data twice during its execution and gets **two different values**.
- A **Phantom Read** is similar to a non-repeatable read but involves **new rows** appearing or disappearing rather than just a single value changing.

If operations are in conflict, they are **not commutable**, meaning if you swap their order, you are "susceptible de conduire à des résultats différents" (likely to get different results).


# Precedence Graph

to see if an entire interleaved execution is "safe" (serializable). To do this, the DBMS builds a **Graphe de précédence**.

This is a visual map of the "dependencies" created by conflicts:

1. **Nodes (Nœuds):** Every transaction involved is represented by a circle (e.g., T1, T2, T3).
2. **Arcs (Arrows):** An arrow is drawn from **Ti → Tj** whenever two transactions have **conflicting operations** on the same data item, and **Ti performs its operation first**.
    - _Think of the arrow as saying: "Ti must logically happen before Tj for the result to remain the same."_

**The Golden Rule of Serializability:**

An execution is **sérialisable** if, and only if, its precedence graph is **acyclique** (has no cycles).

- **No Cycle:** If the arrows only go in one direction (e.g., T1 → T2), the execution is safe. It is equivalent to running them in that specific serial order.
- **A Cycle exists:** If the arrows loop back (e.g., T1 → T2 and T2 → T1), the execution is **non-sérialisable**. This means the transactions are so tangled up that the result is guaranteed to be inconsistent.

![[image-369.png]]
![[image-370.png]]
![[image-371.png]]

# Concurrency Control Algorithms

The DBMS uses a module called the **Ordonnanceur (Scheduler)** to manage the flow of operations. Its job is to reorder or delay operations to ensure the execution remains **serializable**. There are two main ways it does this:

## Le Verrouillage (Locking)

This is a **pessimiste** approach. The system assumes conflicts are likely to happen, so it "locks" data before a transaction can use it.

A lock is a variable associated with every object in the database . Its goal is to block other transactions that want to access a record while it is currently being updated or used. *aka when writing to a variable it gets locked and during it no other transaction can read it or write to it until the lock is over*

The basic principle follows these steps:

1. **Check:** Before modifying data X, the transaction checks if X is already locked by another user.
2. **Wait:** If it is locked, the transaction must wait until the lock is released.
3. **Lock:** Once free, the transaction places its own lock on X.
4. **Modify:** It performs its operation (Read or Write).
5. **Release:** It removes the lock, which allows the system to serve a blocked transaction.

### Types of Locks and Compatibility

To allow for some level of concurrency, the system uses different types of locks:

- **Shared Lock (S - Verrou partagé):** This lock is used for **reading** operations. Multiple transactions can hold a shared lock on the same data item at the same time. It essentially says, "I am reading this, and while I am, others can read it too, but nobody can change it."
- **Exclusive Lock (X - Verrou exclusif):** This lock is used for **writing** (updating or deleting) operations. Only one transaction can hold an exclusive lock on a data item. While a transaction holds an X lock, no other transaction can place **any** type of lock (S or X) on that same item.

- **Note**: a single transaction can hold S and X locks on a single variable, but this cant be the case for 2 different transactions

### Two-Phase Locking (2PL)

#### Phase 1: The Growing Phase

In this first stage, the transaction is strictly in "collection mode".

- **Acquisition:** The transaction requests a **Shared Lock (S)** for every item it needs to read and an **Exclusive Lock (X)** for every item it needs to write.
- **Waiting:** If the requested data is already locked by another transaction with an incompatible lock (such as trying to get an X lock on an item that has an S lock), the transaction must wait.
- **Constraint:** During this phase, the transaction **cannot release any locks**. It can only add to its "inventory" of permissions.

The **Lock Point** is the specific moment when the transaction has successfully acquired the very last lock it requires for its entire sequence of operations. At this exact microsecond, the transaction holds its maximum number of locks and is ready to begin the second phase.

#### Phase 2: The Shrinking Phase

This stage begins the moment the transaction releases its **first lock**.

- **Release:** The transaction can now start releasing locks on data items as it finishes using them. This "frees up" those items for other transactions that might be waiting in the queue.
- **The Point of No Return:** Once this phase starts, the transaction is **forbidden from requesting any new locks**. If it discovers it needs to access a new variable, it is too late; it cannot acquire the lock and will likely have to be canceled and restarted.

#### Example

| Step  | Transaction | Operation | Lock Mechanism Action               | Result / 2PL Status                                                                    |
| ----- | ----------- | --------- | ----------------------------------- | -------------------------------------------------------------------------------------- |
| **1** | T1​         | l1​[x]    | Request **Shared Lock (S)** on x    | **Granted**. T1​ enters its **Growing Phase**.                                         |
| **2** | T2​         | l2​[y]    | Request **Shared Lock (S)** on y    | **Granted**. T2​ enters its **Growing Phase**.                                         |
| **3** | T1​         | e1​[y]    | Request **Exclusive Lock (X)** on y | **Blocked**. Conflicting with T2​’s S-lock on y. T1​ must wait.                        |
| **4** | T2​         | e2​[y]    | Request **Exclusive Lock (X)** on y | **Granted**. The system performs an **upgrade** of T2​'s existing S-lock to an X-lock. |
| **5** | T2​         | c2​       | **Commit** and release all locks    | **Success**. T2​ enters its **Shrinking Phase**, freeing y for other users.            |
| **6** | T1​         | e1​[y]    | Request **Exclusive Lock (X)** on y | **Unblocked**. T1​ is now granted the X-lock it was waiting for.                       |
| **7** | T1​         | c1​       | **Commit** and release all locks    | **Success**. T1​ finishes and releases its remaining locks on x and y.                 |

### Strict 2PL

the most common version used in modern database systems like Oracle

**Strict 2PL:** A transaction **never** releases its locks (specifically its **Exclusive (X) locks**) during the middle of its execution. It holds every single lock until the transaction officially ends with a **Commit** or **Rollback**.

## Optimisites

The **Optimistic** approach to concurrency control is based on the assumption that conflicts between transactions are **rare**. Unlike the pessimistic approach, which proactively blocks data access, the optimistic approach allows transactions to run freely and only intervenes if it detects an actual conflict.

The most common implementation of this approach is the **Timestamping (Estampillage)** algorithm.

### The Principle of Timestamping

Every transaction is assigned a unique, increasing **Timestamp E(Ti)**) based on its start time. The system also tracks two values for every piece of data (X) in the database:

- El(x) **(Read Timestamp):** The timestamp of the youngest transaction that has **read** X.
- Ee(x) **(Write Timestamp):** The timestamp of the youngest transaction that has **written** to X.

The goal is to ensure that conflicting operations always occur in the chronological order of their timestamps.

#### How it works?

When a transaction attempts an operation, the system verifies the following rules:

- **Read Operation:** If your transaction's timestamp is smaller than the data's **last write** (E(Ti​)<Ee(x)), you are rejected because you are trying to read an "old" version of data that has already been updated by a younger transaction.
- **Write Operation:** You are rejected if your timestamp is smaller than the **last read** OR the **last write** (E(Ti​)<El(x) or E(Ti​)<Ee(x)). This prevents you from overwriting data that younger transactions have already seen or modified.

#### What happens when a conflict is catched?

The system undoes every **Écrire (Write)** operation that the transaction performed, restoring the data to exactly how it looked before the transaction started. it will  be automatically resubmitted to the system. However, it is given a **new, younger timestamp**,. This gives it a fresh "age" so it can try to access the data again, hopefully without conflicting with the same transactions as before.

#### Advantages and disadvantages

- **Advantages:** It is faster in low-conflict environments because it eliminates the need to manage locks and completely prevents **Deadlocks (Interblocages)**.
- **Disadvantages:** the risk of **cascading rollbacks** (annulations en cascade), where canceling one transaction forces the cancellation of others that relied on its data.

## The problems of locking

- **Interblocage (Deadlock):** This occurs when two or more transactions are stuck in a circular wait. For example, if Transaction T1 holds a lock on x and needs to access y (which is locked by T2), while T2 simultaneously needs to access x, neither can proceed. To resolve this, systems often use a **Timeout** to cancel the blocked transaction after a certain period
- **Performance:** The management of locks can be inefficient depending on the level of granularity:
	- **Record-level locking** can be very **costly** for the system to manage
	- **Table-level locking** results in **significant wait times**
- **Famine(starvation)**: image a transaction requesting a write(*Exclusive*) lock , but it has to wait because its blocked by a read(*Shared*) lock from an another transaction. If a continuous stream of new transactions (T4​,T5​,T6​...) keeps arriving and requesting Shared locks, the record is never fully "free." Consequently, T1​ stays blocked indefinitely because there is always at least one reader holding a Shared lock.

# Transactions in oracle

## Transaction Validation and Cancellation

- The `COMMIT` command is used to permanently validate and save all changes made during the current transaction.
- A **SAVEPOINT** acts as an intermediate marker or "bookmark" within a transaction. It allows you to divide a long transaction into smaller parts so that you can undo specific operations without having to cancel the entire transaction from the beginning.
	- **Syntax:** `SAVEPOINT savepoint_name;`.
	- **Purpose:** It provides a point of reference for the `ROLLBACK` command, allowing you to return the database to a specific state while keeping the transaction active.
- The **ROLLBACK** command is used to cancel changes made during a transaction, effectively undoing operations and returning the data to a previous consistent state.
	- **Syntax:** `ROLLBACK [ WORK ] [ TO [SAVEPOINT] savepoint_name | FORCE ’commentaire’ ];`.
	- **Complete Cancellation:** If used without the `TO SAVEPOINT` clause, it undoes all changes made since the very beginning of the transaction or the last `COMMIT`.

### how to end transaction

A transaction in Oracle can end automatically without the user explicitly typing `COMMIT` or `ROLLBACK`. The sources identify several scenarios where this happens:

- **Disconnection:** If you manually disconnect from the database, the current transaction is automatically **validated (committed)**.
- **System or Program Errors:** In the event of a system failure or a program exception, Oracle automatically performs a **Rollback** to cancel the active transaction and maintain data consistency.
- **Data Definition Language (DDL)** commands—such as `CREATE`, `DROP`, `ALTER`, or `TRUNCATE`—behave differently than standard data updates (DML like `INSERT` or `UPDATE`) because they trigger an **automatic validation**.

## Isolation level

Oracle provides specific isolation levels to manage how transactions interact with one another, allowing developers to balance **data consistency** with **system performance**. While the standard SQL definition includes four levels, Oracle primarily focuses on two main options

- Under the **READ COMMITTED** isolation level, which is the default setting in Oracle, a transaction is restricted to reading only data that has been officially finalized with a `COMMIT`.
- While **READ COMMITTED** (the default) allows some inconsistencies like non-repeatable reads to favor speed, **SERIALIZABLE** focuses on making the execution of concurrent transactions appear as if they were running one after another in a serial order.

| Isolation Level    | Dirty Read    | Non-Repeatable Read | Phantom Read  |
| ------------------ | ------------- | ------------------- | ------------- |
| **READ COMMITTED** | **Prevented** | Possible            | Possible      |
| **SERIALIZABLE**   | **Prevented** | **Prevented**       | **Prevented** |

### Transaction syntax

The **SET TRANSACTION** command is used to define the specific characteristics of the current transaction before any data operations begin.

```SQL
SET TRANSACTION [ READ ONLY | READ WRITE ]

[ ISOLATION LEVEL [ SERIALIZE | READ COMMITED ]]
[ USE ROLLBACK SEGMENT ’segment name’ ]
[ NAME ’transaction name’ ];
```


## Hierarchical Locking

1. **Downward Locking (Top-Down)**

- **The Goal:** To lock the **entire table** at once.
- **How it works:** You place a heavy lock (like **Exclusive (X)** or **Shared (S)**) directly on the table.
- **The Effect:** Because of the hierarchical principle, this lock automatically "flows down" to every row. You don't need to lock the rows individually because the table-level lock makes the entire contents of the table your "territory".
- **Use Case:** This is usually used for big maintenance tasks where you don't want anyone else touching any part of the table while you work.

**2. Upward Intention Locking (Bottom-Up)**

- **The Goal:** To lock **specific rows** while protecting the table from being locked as a whole.
- **How it works:** You place a lock on a **specific row** (like an Exclusive (X) lock to update a salary). However, before you can do that, you must first place an **Intention Lock** (like **IX** or **IS**) at the table level.
- **The Effect:** The table-level lock here is just a **signal (a flag)**. It doesn't stop others from reading or writing different rows; it only stops someone else from trying to perform a "Downward Lock" (like locking the entire table for maintenance) while you are still working on your row.
- **Use Case:** This is the standard "concurrency" mode used for daily operations (INSERT, UPDATE, DELETE), allowing many people to work on different rows in the same table simultaneously.

**Summary Comparison**

| Feature             | Downward Locking                                  | Upward Intention Locking                            |
| ------------------- | ------------------------------------------------- | --------------------------------------------------- |
| **Primary Target**  | The **entire Table**.                             | **Specific Rows**.                                  |
| **Table Lock Role** | It is the **main lock** that controls all rows.   | It is a **signal (flag)** of your intent.           |
| **Concurrency**     | **Low** (stops everyone from touching the table). | **High** (allows others to work on different rows). |
| **Logic**           | "I have the table, so I also have the rows".      | "I have a row, so I must flag the table".           |

![[image-372.png]]

