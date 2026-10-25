
# Objective

The need for a robust recovery system arises from the fact that modern Database Management Systems (DBMS) are **multi-user environments**. Multiple users submit transactions that execute concurrently, and the system must ensure these do not interfere with each other or produce incorrect results.

- **he Goal of Isolation:** The system must provide the illusion that each transaction is executing in total isolation, even when many are running at once.
- **The Risk of Inconsistency:** If a software or hardware error occurs between the start and end of a transaction, the database risks falling into an **inconsistent state**. This could be caused by a database server crash, a specific transaction error, a program exception, or a physical disk failure.
- **Recovery Objective:** The primary objective of recovery (_Recouvrement_) is to ensure that failures do not leave the database in an incoherent state. The DBMS must be able to restore the database to the state most closely resembling its condition just before the crash.
- **Ensuring Atomicity:** To maintain **Atomicity**, the DBMS must guarantee that if a transaction fails, all its partial modifications are completely canceled. This is supported by the `COMMIT` and `ROLLBACK` mechanisms we discussed in the previous chapter.

#  Types of failures

- **Light Failure (Panne légère):** This type of failure affects the **volatile RAM** of the data server but does **not affect the disks**.
    - **Common Example:** A database server crash.
    - **Recovery Method:** Since the disks are intact, the system uses the **UNDO/REDO** algorithms to restore consistency by processing the transaction logs.
- **Heavy Failure (Panne lourde):** This is a more severe malfunction that **affects a physical disk**.
    - **Common Example:** A disk becoming "HS" (Hors Service/Dead).
    - **Recovery Method:** Because data on the disk may be lost, recovery requires a combination of a **full backup (dump)** and the **transaction logs** to reconstruct the database state.

The sources also characterize these as **Catastrophic** vs. **Non-Catastrophic** failures. A non-catastrophic failure only requires canceling the operations that caused the inconsistency using log entries, whereas a catastrophic failure requires reinstalling a version of the database from a backup copy before exploiting the logs.


# Storage management

## before and after images

- **After Image (Image Après):** This refers to the data as it appears **after** it has been modified by a transaction. To guarantee a **Commit**, this "after image" must eventually be written to the physical disk to ensure the changes are permanent.
- **Before Image (Image Avant):** This refers to the original data as it existed **before** the modification began. To guarantee a **Rollback**, this "image avant" must be available on the disk so the system can restore the original state if the transaction fails.
- **The State of the Database:** At any given time, the official "state" of the database is the sum of all transactions validated since the beginning. the state of the database **MUST ALWAYS BE ON THE DISK**

## physical level of the DB

![[image-378.png]]

DBMS does not work directly on the physical disk for every operation because it would be too slow. Instead, it uses a **buffer (or cache)** system to manage data movement between volatile memory and persistent storage.

- **Logical vs. Physical Operations:** The SGBD performs "logical" reads and writes within the **Base Cache** (volatile memory). Physical reads and writes only occur when data is moved between this cache and the **Base Disk** (persistent storage).
- **Buffer Primacy:** A portion of the database is copied into the buffer, and **all updates are performed in the buffer first** before they are synchronized with the disk.
- **Replacement Strategy (LRU):** Because the buffer has limited space, the system must decide which data to remove when the memory is full. The most common algorithm used is **Least Recently Used (LRU)**.
    - The system identifies a "victim" block—the one that hasn't been accessed for the longest time.
    - This "victim" is removed from the central memory to make room for a new block.

## Saving data from memory to disk

![[image-379.png]]

- **The Version Shift:** Until the moment of a **commit**, the "Before Image" (the original data) is considered the official part of the database state. At the moment of the commit, the "After Image" (the modified data) must replace the "Before Image".
- **The "All or Nothing" Problem:** The core difficulty is ensuring this replacement is **atomic**. In computing, atomicity means the operation must either complete entirely or not happen at all.
- **The Risk of Failure:** If a crash occurs precisely while the system is overwriting the "Before Image" with the "After Image" on the physical disk, the data could become corrupted—leaving the database with a "half-written" value that is neither the old nor the new version.
- **Requirements for Consistency:**
    - To **guarantee a commit**, the "After Image" must be safely on the disk.
    - To **guarantee a rollback**, the "Before Image" must be safely on the disk.

This technical hurdle is why simple disk writes are insufficient and why databases must use specific synchronization strategies and transaction logs.


## Update Synchronization Strategies

### Immediate Update (Mise à jour immédiate)

![[image-380.png]]

The **Immediate Update** strategy is the most direct approach to synchronization. In this mode, as soon as a data block is modified in the buffer, the system immediately writes that change to the physical disk.

- **Mechanism:** Every time a transaction performs a "write" operation in the volatile memory, the system triggers a corresponding physical write to the disk to keep them synchronized.
- **Advantages:** Its primary advantage is **simplicity**. Because the disk always reflects the most recent changes, the system doesn't have to manage a large backlog of pending writes.
- **Disadvantages:**
    - **Low Performance:** It is considered inefficient because it forces the disk to perform many **random writes** (_écritures aléatoires_) rather than waiting to write data in a more organized way.
    - **Loss of Original Data:** By writing immediately, the system **overwrites the "before image"** on the disk. If the transaction later needs to be rolled back, the original data is already gone from the persistent storage.
- **Recovery Requirement:** Because the "before image" is overwritten before a commit is finalized, this strategy strictly requires an **UNDO** mechanism to restore the original values if a failure occurs.

### Deferred Update (Mise à jour différée)

![[image-381.png]]

the **Deferred Update** approach follows a strict rule: the system **forbids writing any modified data blocks to the disk before the transaction officially commits**.

Here is how this strategy functions and its impact on the system:

- **Preservation of the "Before Image":** Because no changes are allowed to reach the disk until the very end, the original data (the **Image Avant**) remains perfectly intact on the physical storage throughout the transaction's life.
- **The Commit Process:** When a transaction reaches its **Commit** point, the system performs a "forced write," transferring all the modified "after images" from the buffer (RAM) to the disk all at once.
- **The Rollback Process:** If a transaction fails or a user triggers a **Rollback**, the process is extremely simple—the system merely **deletes the modified blocks from the buffer**. Since nothing was ever written to the disk, the database automatically remains in its original, consistent state.
- **The Main Disadvantage:** The primary risk of this strategy is **buffer saturation**. Since the system is prohibited from clearing space by writing modified blocks to the disk, the volatile memory (RAM) can quickly become overloaded if transactions are large or long-running.
- **Recovery Requirement:** In the event of a crash, the system strictly requires a **REDO** mechanism. This is because a transaction might have officially "committed" in the log, but the system may have crashed before those changes were physically pushed from the buffer to the database disk.

### Opportunistic Update (Mise à jour opportuniste)

![[image-382.png]]

The **Opportunistic Update** strategy is described as the most flexible and efficient method for synchronizing data between the volatile buffer and the physical disk.

- **Mechanism:** The system waits for the **best opportunity** to synchronize the buffer and the disk. This means it can group several modifications together or wait until the system is less busy to perform the physical write.
- **Performance Benefits:** It is the **least penalizing** strategy for system performance. It allows for "successive writes" within the buffer—meaning a piece of data can be updated multiple times in RAM before the final version is eventually saved to the disk in a single operation.
- **The Overwriting Risk:** Because the system is "opportunistic," it might decide to write a block to the disk even if the transaction hasn't committed yet. If this happens, the **"before image" is overwritten**, which would normally make recovery impossible if the transaction later needed to be rolled back.
- **Why It Is Preferred:** Despite the risks, it is the preferred mode in modern databases because it avoids the two major pitfalls of the other strategies: it doesn't **overload the buffer** like the deferred mode, and it avoids the **slow, random disk writes** of the immediate mode.
- **Recovery Requirements:** To use this high-performance mode safely, the system strictly requires both **UNDO and REDO mechanisms**. Additionally, it relies entirely on the **Transaction Log (Journal)** to keep track of changes so that the "before" and "after" images can be reconstructed if a crash occurs.

# The Transaction Log (Journaling)

![[image-383.png]]
![[image-384.png]]
it is a supplementary file that acts as a secure history of every modification made to the database.

The log is designed with specific technical properties to ensure that it remains a reliable source of truth, even when the main database might be inconsistent.

- **Sequential Structure:** Unlike the database disk, which uses random access for performance, the system writes to the log **sequentially**. This makes writing to the log extremely fast and efficient.
- **Permanent Record:** A critical rule of journaling is that the system **never deletes** an entry from the log; it only appends new information to the end of the file.
- **Dedicated Buffer:** The log has its own **separate buffer** in the volatile memory. While the main database uses "opportunistic" writing to favor speed, the log uses **immediate and forced writing** to the disk to ensure that the history of changes is never lost in a RAM failure.

**Standard Log Entries:** Each line in the log follows a specific format to allow the recovery algorithms to reconstruct the database state:

- **start(T)**: Marks the beginning of transaction T.
- **write(T, x, old_val, new_val)**: Records that transaction T changed variable **x** from its **old_val** (before image) to its **new_val** (after image).
- **commit(T)**: Signals that transaction T was successfully completed.
- **rollback(T)**: Signals that transaction T was cancelled.
- **checkpoint**: A special marker indicating a moment when all previous modifications were synchronized to the database disk.

The sources note that the `write` operation can be recorded either **logically** (the SQL instructions used) or **physically** (the actual data records).


## Write-Ahead Logging (WAL)

![[image-385.png]]

It dictates that **any modification to a data block must be recorded in the transaction log** **before** **that modified block is physically written to the database disk**.

- **The Core Logic:** The system must ensure that the "before image" (the original value) is safely stored on persistent storage (the log disk) before the original value on the database disk is overwritten by the "after image".
- **The Risk of Violation:** If the WAL rule is violated—for example, if the system writes a new value to the database disk but crashes before recording it in the log—the system loses all trace of the previous value. In this scenario, it becomes **impossible to perform a rollback** or restore the database to a consistent state.
- **A Key Consequence:** Because of this rule, the transaction log often contains records of modifications that have not yet been "committed" or validated. This is perfectly normal and is why the **UNDO** algorithm is necessary during recovery to clean up these uncommitted changes.
- **Summary Principle:** "Before writing in the base → write in the log".

## The Point of Commit

The **Point of Commit** is a fundamental rule that defines the exact moment a transaction is considered permanently successful and "safe" from a system failure. this rule dictates that at the moment of a commit, the system **forces the writing of all modifications into the transaction log**.

- **The Validation Threshold:** A transaction is not officially validated just because the user types "COMMIT" or because the operations finish in the buffer. It is only considered validated **when the** **commit(T)** **instruction is physically written onto the log disk**
- **Consequence for Recovery:** If a crash occurs, the recovery system looks at the log. If it finds the `commit` record for a transaction, it knows that the data **must** be preserved (using the REDO process). If it doesn't find that record, the transaction is treated as if it never happened (using the UNDO process).

# Recovery algorithms

When a system restarts after a light failure (RAM loss), the recovery manager must immediately reconstruct the state of all transactions that were running at the time of the crash. This process is entirely based on the information stored in the transaction log.

## Identifying Transaction Lists

The first step in any recovery algorithm is to scan the log to categorize all transactions into two distinct lists.

- **List of Validated Transactions (LV​**): This list contains all transactions for which a **commit(T)** record is found in the log. These are transactions that the system promised to save permanently, so their changes must be preserved.
- **List of Active or Cancelled Transactions (LA​**): This list includes any transaction that appears in the log (with a `start(T)`) but **does not have a corresponding** **commit(T)** entry. These are treated as incomplete or failed transactions whose partial effects must be removed from the database to maintain atomicity.

By analyzing these lists, the system also identifies the **Image Avant** (old value) and **Image Après** (new value) for every modification performed by these transactions, allowing the recovery manager to decide exactly what to "undo" or "redo".


## The Undo Process

The **Undo process** is designed to maintain the **Atomicity** of transactions by ensuring that any changes made by uncommitted or failed transactions are completely removed from the database.

- **Target Group (LA​**): This algorithm specifically targets transactions in the **List of Active or Cancelled Transactions (LA​**)**—those that appear in the log but lack a `commit(T)` entry.
- **The "Old Value" Rule:** For every modification recorded as `write(T, x, old_val, new_val)`, the Undo process takes the **old_val** (the "Before Image") and writes it back into variable **x**.
- **The Rule of Reverse Order:** A critical technical detail in the sources is that the Undo algorithm must process transactions in the **reverse order of their initial execution**.
    - _Why reverse order?_ This ensures that if a variable was modified multiple times by uncommitted transactions, the database is correctly "rolled back" through its previous states until it reaches the last known consistent value from before those transactions started.

## The Redo Process

the redo is used to maintain the **durability** of the transactions by ensuring that commited transactions are permanent

**Target Group (LV​**): This algorithm specifically targets transactions in the **Validated transactions** those are the transactions that appear in the log and contain a commit operation at the end of them
- **The "Old Value" Rule:** For every modification recorded as `write(T, x, old_val, new_val)`, the redo process takes the operation and writes it again effective storing the new value inside of x
- **The Rule of Reverse Order:** A critical technical detail in the sources is that the Redo algorithm must process transactions in the **Same order of their initial execution**.

## Checkpoints


![[image-386.png]]

**checkpoints** are a mechanism used to optimize the database recovery process after a failure. Without them, a system would theoretically need to re-execute every transaction recorded in the log since the database was first created, which is far too costly and inefficient.

**How Checkpoints Work**

When a checkpoint occurs, the system performs the following actions:

- **Disk Synchronization:** It writes all modified blocks currently in the buffer (RAM) onto the physical disk.
- **Validation Guarantee:** This process guarantees that all data validated by a `commit` up to that point is safely stored in the database on the disk.
- **Log Recording:** A "checkpoint" entry is recorded in the transaction log. This entry typically includes a list of transactions that were active at the time of the checkpoint.

**Role in Recovery**

The primary purpose of a checkpoint is to **limit the amount of work** required during a recovery operation (Undo/Redo).

- **Starting Point:** When a failure occurs, the recovery process does not start from the beginning of the log; instead, it only takes into account transactions and log entries that have occurred **since the last checkpoint**.
- **Efficiency:** By ensuring that all prior committed data is already on the disk, the system only needs to focus on redoing (Redo) transactions that were committed after the checkpoint and undoing (Undo) those that were active or failed at the time of the crash.

## Disk failures

![[image-387.png]]
![[image-388.png]]
so far we have seen memory buffer failues, but what happens when a failure happens at the DB disk? 

The primary defense against disk failures is **replication**. For this to be effective, it is **imperative** to store the database files and the transaction log on **two distinct disks**. If they are on the same physical disk and it fails, the system loses both the data and the history needed to recover it.

If the disk containing the database files fails, there are two main ways to recover:

- **Basic Solution:** Reinstall a new disk and **re-execute every transaction** recorded in the log since the database was first created. This is often impractical because the restart latency is very long and it requires keeping logs from the very beginning.
- **With Backups (Sauvegarde):** A "dump" or backup (St​) is a copy of the database at a specific time t. To recover, you restore the backup and then **re-apply only the log entries** that occurred from time t until the failure.

## Log failures

![[image-389.png]]

If the disk containing the transaction log fails, the state of the database is still technically available in the database files and the RAM buffer.

- **Recovery:** The system manages this by performing a **checkpoint** to write all modified blocks currently in the buffer onto the database disk, followed by necessary repairs and a restart.
- **Risk:** This method is "fragile." For example, if a power failure and a log disk failure happen at the same time, data could still be lost.
- **Advanced Protection:** To prevent this, systems can **replicate the log** itself onto multiple disks, which is a key motivation for moving toward distributed systems.


