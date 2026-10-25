
# Data storage

##  Defintion

Data storage includes all **methods and technologies** to save digital data long-term so it can be accessed later
It's a combination of **hardware** (disks, servers, networks) + **software** that handles large amounts of information.

##  Objectifs of data storage

- **Integrity:** The data must be able to **survive hardware incidents**. The goal is to provide a theoretically infinite lifespan for the information.
- **Security:** The system must be able to **control and track all access** to the data, ensuring only authorized people can read, write, or create information.
- **Performance:** The architecture must be fast enough to meet the users' needs in terms of **throughput** (how much data moves) and **latency** (the delay before data starts moving).
- **Transparency:** Ideally, a user should **not need to know where or how** the data is physically stored on the disks to be able to access it.
- **Cost Limitation:** A good architecture should allow for the storage of **massive volumes of data** while keeping the expenses for setup and maintenance as low as possible.

# Memories

there are 2 types of memories:

- **Volatile Memory:** This is fast, temporary memory. It only holds onto information as long as the computer has power. **As soon as the system is turned off or there is a power failure, all the data in volatile memory is lost**.
- **Persistent (Non-Volatile) Memory:** This is memory that can keep its content even when there is no power supply. Databases rely on persistent memory (like hard drives) to ensure that records aren't lost every time the server restarts.

## Memory hierarchy

![[image-285.png]]

- **Primary Memory (Volatile):** This is the memory used directly by the CPU.
    - **Cache Memory:** Extremely fast but very small. The CPU uses it to speed up program execution.
    - **Main Memory (RAM):** The main workspace where the CPU loads data and instructions to work on them. It is slower than cache but much larger. **Important:** Primary memory is expensive and its capacity is usually smaller than what a full database requires.
- **Secondary Memory (Persistent):** This is the "online" storage for the database.
    - **Magnetic Disks (HDD):** These use rotating magnetic surfaces to store large amounts of data.
    - **Solid State Drives (SSD):** These use flash technology and have no moving parts, making them much faster than traditional disks.
- **Tertiary Memory (Archival):** This is the slowest level, used for long-term archiving and backups.
    - Examples include **Optical Disks (CD/DVD)** and **Magnetic Tapes**, which offer the largest capacity at the lowest cost.

**Summary**

```
PRIMARY (fast, expensive, volatile):
├── Cache (10^-8s, MO) → CPU uses for instructions
└── Main RAM (10^-7s, GO) → Working data

SECONDARY (slower, cheaper, persistent):
├── Flash/SSD (10^-4s, TO, very fast)
└── Magnetic disks (10^-2s, TO, standard)

TERTIARY (slowest, cheapest, archival):
├── Optical disks (CD/DVD)
└── Magnetic tapes
```

**Note**:

Data stored on secondary or tertiary levels **cannot be processed directly by the CPU**. To work with any piece of data, the DBMS must first copy it from the disk into the **main memory** (primary memory) so the CPU can access it.


## Memory performance

### Access Time (Temps d'accès)

- Time to reach a specific memory location and get the data
- **Critical for random access** (like finding student ID #5634)

```
Cache:      10^-8 sec (0.01 microseconds)   
RAM:        10^-7 sec (0.1 microseconds)   
SSD:        10^-4 sec (0.1 milliseconds)   
Disk:       10^-2 sec (10 milliseconds)
```

### 2. Throughput/Transfer Rate (Débit)

- Amount of data read per second in **best case** (sequential reads)
- **Critical for sequential access** (reading a whole table)

```
Cache:      10+ GB/s  
RAM:        Several GB/s  
SSD:        Several GB/s  
Disk:       100 MB/s
```

##  Magnetic disk

![[image-286.png]]

### Physical Construction

- **Platters:** A disk is made of several rotating magnetic surfaces called platters.
- **Read-Write Heads:** A mechanical arm moves across these platters to read or write data using a process of **magnetization**. Each platter usually has its own dedicated head.

### Logical Organization

To manage data efficiently, the disk surface is divided into specific areas:

- **Tracks:** These are circular divisions (rings) on each platter.
- **Sectors:** Each track is divided into "slices" called sectors, which typically have a fixed size of **512 bytes**.
- **Blocks:** The DBMS groups several sectors together into **Blocks** (or pages). **Crucial Point:** The block is the **actual unit of transfer** (I/O) between the secondary memory (disk) and the primary memory (RAM).
- **Cylinders:** This is a "virtual" concept. It represents the set of all tracks that are at the **same position** on every platter.

### Performance and Access Time

Whenever the DBMS needs to read or write a block, the total **Access Time** is determined by three mechanical delays:

1. **Seek Time (Positioning):** The time needed to move the mechanical arm to the correct track.
2. **Latency:** The time spent waiting for the disk to rotate so the specific block passes under the head.
3. **Transfer Time:** The actual time it takes to move the data from the disk to memory.

![[image-288.png]]

**Pro-tip for Performance:** To make the database faster, we try to place related data in the **same sector, then the same cylinder, or adjacent cylinders**. This minimizes the physical movement of the mechanical arm, which is the slowest part of the process.

# Raids

![[image-289.png]]

## Defintion

**RAID** = _Redundant Array of Inexpensive Disks_. Combines multiple disks into **one logical unit** for **better performance + data protection**

**3 main benefits**:

- **Performance**: Parallel reads/writes across disks
- **Redundancy**: Survive disk failures
- **Capacity**: Use cheap disks efficiently

## Raid 0

This configuration splits data across multiple disks. It is very fast because the system can read from all disks at once, but it offers **no security**. If even one disk fails, **all data in the entire array is los**

- all of the memory

## Raid 1

Every piece of data is written to two or more disks simultaneously so they are exact copies. This provides **excellent protection** because if one disk breaks, the other has a perfect copy. However, it is **expensive** because you only get the storage capacity of one disk, no matter how many mirrors you have.

- only a single disk can be filled

## Raid 5

This is a compromise between speed and security. It requires at least **three disks**. It spreads data across the disks but also includes "parity" information. If one disk fails, the system can use that parity information to **reconstruct the missing data**.

- number of disks minus 1

## SCSI

This is a standard bus used to connect computers to peripherals.

- It is **faster and more complex** than older interfaces (like E-IDE) because the connected devices can process complex instructions.
- It offers speeds up to **640 Mo/s**.
- However, it has limitations: cables can only reach **20 meters**, and it is generally limited to **point-to-point** connections.

## Fibre channel

Originally designed for super-computers, this has become the standard for modern high-performance storage networks. It supports three different layouts (topologies):

![[image-290.png]]


1. **Point-to-Point:** Two devices connected directly with dedicated bandwidth.
2. **Loop (FC-AL):** Up to **126 devices** connected in a ring managed by hubs.
3. **Switched (Fabric):** Uses a Fibre Channel switch (similar to an Ethernet switch) to connect devices. This is the most powerful version, allowing for a theoretical maximum of **16 million components**.

# Files organization

**How databases store actual data on disk** - the lowest level.

## Record (Enregistrement)

**One row in a table** = one record. Contains field values (columns).

```
FIXED SIZE: All fields same size (INT=4 bytes, CHAR(10)=10 bytes)
Example: ID(4) + Name(20) + Age(4) = 28 bytes always

VARIABLE SIZE: VARCHAR fields, NULLs
Example: ID(4) + Title("Vertigo"=7 bytes) + Year(NULL) 
Header stores: length, NULL bitmap, schema pointer
```

**Fixed size**

![[image-291.png]]

**Variable size**

![[image-292.png]]

## Blocks

As we discussed earlier, the **block is the unit of transfer** between the disk and the RAM. A single block contains multiple records.

### Block placement and splitting

When fitting records into blocks, the system has two choices:

![[image-293.png]]

- **Non-fractioned (Unspanned):** Every record must fit entirely within one block. If a record is too big to fit in the remaining space of "Block A," that space is left empty (wasted), and the record starts at the beginning of "Block B".
- **Fractioned (Spanned):** If a record is larger than the block size, or if the system wants to avoid wasting space, a record can be **split across two blocks**. In this case, the first block contains a **pointer** directed to the next block where the rest of the record is located

### General structure of a block

- **he Header (Entête):** This acts as the "management office" for the block. It contains a **directory of pointers** that tell the system exactly where each record starts within the block, as well as **chaining information** (a pointer to the next block in the file).
- **The Data Zone:** This is the collection of "cells" where the actual records are stored.

### if records are variable sized

![[image-294.png]]

the size of the header is not fixed and it contains pointers to its records and a pointer to the next page, the records are placed at the top and at the bottom we have a free space area

### if records are fixed sized

![[image-295.png]]

the head size is fixed and it contains the number of records and indicateurs to them ***either 1 or 0*** to show whether they are occupied or not

# Primary File Organization

**How entire files (tables) are organized across many disk blocks.** 4 main types :

## Heap File (Fichier séquentiel non ordonné)

![[image-296.png]]

This is the simplest possible structure. New records are simply added at the end of the file as they arrive.

- **Performance:**
    - **Insertion:** Very low cost because the system just appends data to the end.
    - **Searching:** Very poor performance. To find a specific record, the system must perform a linear scan. On average, it must access b/2 **blocks** (where b is the total number of blocks in the file), and in the worst case, it must scan all b **blocks**.
- **Best use:** High-speed data logging where you rarely need to search for specific items.

```
Records added to END of file (like a pile/heap)
No order by any field
```

## Sorted Files (Fichier séquentiel trié)

In this structure, records are physically ordered on the disk based on the value of a specific field, called the **sort key**.

- **Performance:**
    - **Searching:** Very fast on the sort key field. It uses a **binary search** (recherche dichotomique) with a complexity of log2​(b), meaning even in a massive file, it only takes a few block accesses to find data.
    - **Insertion:** Very costly. Because the physical order must be maintained, the system often has to "shift" existing records to make room for a new one in the middle of the file.
- **Best use:** Data that is queried frequently but updated rarely.

## Hashed Files (Fichier haché)

Instead of an order or a sequence, the system uses a mathematical **hash function** applied to a specific field (the hash key) to calculate the exact address (block) where a record should be stored.

- **Collisions:** A "collision" occurs when the hash function points a new record to a block that is already full.
- **Resolving Collisions:** The system can resolve this by searching for the first free spot, applying a second hash function, or placing the record in a **linked overflow zone** (zone de débordement).
- **Performance:** Extremely fast for direct access if you have the key, but performance degrades if there are too many collisions.

```
h(title) = rank(first letter) mod 5
"Citizen Kane" → rank('C') mod 5 = 3 → Block f3 (full → overflow)
```

![[image-297.png]]
## Other Structures (B-Trees)

which are the most common structure used in modern databases. They are balanced tree structures that keep data sorted and allow for **logarithmic time** for searches, insertions, and deletions.

|Organization|Insert|Lookup|Range Scan|Use Case|
|---|---|---|---|---|
|**Heap**|Fast|Slow|Slow|Logs|
|**Sorted**|Slow|Fast|Fast|Directories|
|**Hash**|Fast|Fast|Poor|Exact key lookup|
|**B-Tree**|Medium|Fast|Fast|**Oracle default**|

# Secondary file organization

**The core problem**: Your table can only be **physically sorted one way**. You can't sort by ID **and** by Name at the same time.

Primary organization is fixed (one table = one method). What if you need **multiple search keys**?
**Solution**: **Secondary indexes** - separate files mapping **any field** → record location.

## Primary index

A primary index is used only when the main data file is **already physically sorted** by a unique key (like a Student ID).

- **Non-Dense Structure:** It is "non-dense," meaning it does **not** contain an entry for every single record. Instead, it only stores the key of the **first record of every block**.
- **The Process:** To find a specific ID, the system looks at the index to find which block that ID _should_ be in. It then jumps directly to that block on the disk and does a quick scan of only those few records. This makes it very fast because the index file itself is tiny compared to the main data file.

![[image-298.png]]

**Note**: A primary index **only searches for the field used to sort the file**. If your data is sorted by "ID," a primary index cannot help you find a "Salary" or a "Name".

## Clustered indexes

A **clustered index** is used when the primary data file is physically sorted by a field that is **not a unique key**, meaning the field can contain duplicate values.

A **clustered index** is used when the primary data file is physically sorted by a field that is **not a unique key**, meaning the field can contain duplicate values.

Here is how they function based on the sources:

- **Structure:** Unlike a primary index that points to every block, a clustered index contains one entry for **every distinct value** found in the sorting field.
- **Function:** Each entry in the index file stores a distinct value and a **pointer to the first block** on the disk where that specific value begins to appear.

![[image-299.png]]

## Secondary record

Used to search by a field that was **not used for the primary sorting** of the file. This index is "dense," meaning it contains an entry for **every single record** in the data file.

![[image-300.png]]

## Multi level indexes

![[image-301.png]]

This structure works by adding **additional levels of indexing on top of the index files themselves**. Here is the detailed breakdown of how they function:

- **Layered Structure:** You can think of this as an "index of an index." The system continues adding levels until the **top-level index can fit entirely within a single block**.
- **Types:** Multi-level indexing can be applied to **primary, secondary, or clustered indexes**.
- **Access Performance:** To find a specific record using this structure, the system must access **N + 1 blocks**, where **N** represents the number of levels in the index. For example, in a 2-level index, the system would access the first index level, then the second, and finally the actual data block.
- **Dynamic vs. Static:** The sources also note that these multi-level structures can be **dynamic**, allowing them to grow and change as the data file expands.

# Oracle data organization

- Physical storage: These are the actual files sitting on your hard drive, such as **Data Files**, **Control Files**, and **Redo Log Files**
- This is how Oracle organizes space internally. The hierarchy from smallest to largest is:

```
DISK → Tablespace → Datafile → Extent → Block (8KB default)
```

## Data block

The **Data Block** is the **smallest unit of storage** managed by an Oracle database. While it is a "logical" structure, it is closely tied to the hardware because its size must always be a **multiple of the operating system's block size**. For example, if a Linux system uses blocks of 1,024 bytes, an Oracle block might be set to 4,096 or 8,192 bytes.

Every Oracle data block is organized into **five specific parts**, regardless of the type of data it stores,:

1. **Header (Entête):** Contains the physical address of the block and the type of information it holds (such as table data or index data).
2. **Table Directory:** A list of the tables that have records stored within this specific block.
3. **Record Directory:** Contains the exact addresses of every individual record currently residing in the block.
4. **Free Space:** A "cushion" of empty space reserved for **inserting new records** or allowing existing records to **expand** (for example, when a field that was previously NULL is updated with a value).
5. **Data Space:** The area where the raw records are actually kept.

**Note**: The management of this space is controlled by two key parameters: **pctfree** (the percentage of the block to keep empty for future updates) and **pctused** (the minimum level of emptiness required before the block can accept new records again).

## extent (extentions)

An **Extent** is a collection of **contiguous data blocks** (blocks that are physically next to each other on the disk).

Here are the key details from the sources:

- **Purpose:** An extent is generally assigned to a single type of data, such as the records for one specific table.
- **Performance:** The fact that the blocks are **contiguous** is essential for speed. It allows the disk's read-write head to scan the data without having to jump around to different parts of the physical disk, which minimizes mechanical delays.
- **Management:** The Database Administrator (DBA) can specify the number of blocks in an extent. When a table needs more room, Oracle doesn't just add one block; it adds a whole new **extent**.

## Segment

A **Segment** is a logical structure that represents a collection of one or more **Extents**. While an extent is just a group of blocks, a segment is created for a **specific purpose** or a specific type of data within Oracle.

According to the sources, there are four main types of segments:

1. **Data Segments:** These store the actual records of a table. Every time you create a table, Oracle creates one data segment for it.
2. **Index Segments:** These store the information for an index. Every index you create gets its own segment.
3. **Temporary Segments:** These are used by Oracle as a "scratchpad" for temporary operations, such as performing a large **sort** during a query.
4. **Rollback Segments:** These are very important for security and recovery. They store the "before" version of data during a transaction. If a power outage occurs before you save (commit), Oracle uses these to **undo** (rollback) the changes and restore the data to its original state.

## Table space

A **tablespace** is the highest logical level of storage in an Oracle database. While segments are logical containers for specific objects (like a single table), a tablespace is a logical container that groups these segments together and maps them to physical storage.

Key characteristics of tablespaces include:

- **Physical Mapping:** A tablespace is made up of **one or more physical data files** on the disk. While the operating system sees the files, Oracle sees the tablespace.
- **The SYSTEM Tablespace:** Every Oracle database always has at least one tablespace created at initialization called **SYSTEM**. This special tablespace contains the **data dictionary**, stored procedures, and triggers.
- **Administrative Control:** The Database Administrator (DBA) uses tablespaces to manage the database efficiently. For example, they can:
    - **Control Availability:** Take a specific tablespace **offline** for maintenance or backups without shutting down the entire database.
    - **Improve Performance:** Distribute data across **multiple physical disks** by placing different tablespaces on different hardware.
    - **Set Quotas:** Limit how much disk space specific users are allowed to use.
    - **Define Defaults:** Set default storage parameters (like the size of new extents) that will apply to any table or index created within that tablespace.

# Files types in oracle

##  data files

in each data base there is atleast a single data file that contains the database data like tables and indexes

## Control files

there are meta data files that contains important information about the data base like its structure and the name of the database....etc

## Redo log  files

- They record **every single modification** made to the data.
- If the system crashes before changes are permanently saved to the disk, Oracle uses these logs to recover the lost information.
- Because they are so vital, Oracle allows "multiplexing," which means keeping multiple copies of these logs on different physical disks for extra safety.

##  other types

-  **Paramters**: they define the configuration on an oracle instance
- **passwords**: store passwords
- **Archive log files**: they contain log files of the redo files created by instances of oracle

# Commands related to  storage

## Views

- La vue DBA_EXTENTS donne la liste des extensions ;
- La vue DBA_SEGMENTS donne la liste des segments ;
- La vue DBA_FREE_SPACE permet de mesurer l’espace libre ;
- La vue DBA_TABLESPACES donne la liste des tablespaces ;
- La vue DBA_DATA_FILES donne la liste des fichiers.

## Alter table space

**To make a tablespace offline (maintenance)**

```SQL
ALTER TABLESPACE TB1 OFFLINE;
```

**To make readonly**

```SQL
ALTER TABLESPACE TB1 READ ONLY;
```

**To change the default storage settings**

```SQL
ALTER TABLESPACE TB1
DEFAULT STORAGE (
NEXT 100K
MAXEXTENTS 200);
```

## Create table space

![[image-302.png]]



```
CREATE TABLESPACE TB2
DATAFILE 'fichierTB2.dat' SIZE 2M
AUTOEXTEND ON NEXT 5M MAXSIZE 500M
DEFAULT STORAGE (INITIAL 128K NEXT 128K MAXEXTENTS UNLIMITED);
```

- **`DATAFILE 'fichierTB2.dat' SIZE 2M`**: This creates a physical file on the hard drive. It starts with an initial size of **2 Megabytes**.
- **`AUTOEXTEND ON NEXT 5M`**: This is a "growth" setting. If the 2MB fills up, the database will automatically add another **5MB** to the file size so you don't run out of space.
- **`MAXSIZE 500M`**: This puts a hard cap on growth. The file will stop growing once it reaches **500 Megabytes**.
- **`DEFAULT STORAGE (...)`**: These are the "rules" for any table created inside this tablespace:
    - **INITIAL 128K**: The first chunk of space given to a new table.
    - **NEXT 128K**: The size of subsequent chunks (extents) given to a table as it grows.
    - **MAXEXTENTS UNLIMITED**: A table can keep growing and grabbing new chunks forever (until the tablespace itself is full).

