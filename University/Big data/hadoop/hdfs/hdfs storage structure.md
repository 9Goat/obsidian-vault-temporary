
# Introduction

**HDFS** is the **storage layer** of Hadoop. It's a distributed file system that stores data across many machines, providing high-throughput access to application data and fault tolerance through replication.


# architecture

HDFS uses a **Master-Slave architecture** with three main components:
![[image-422.png]]

```text
┌─────────────────────────────────────────────────────────────┐
│                  HDFS ARCHITECTURE                          │
│                  (Master/Slave Model)                       │
└─────────────────────────────────────────────────────────────┘

                        ┌─────────────┐
                        │   SNN       │
                        │ (Secondary  │
                        │  NameNode)  │
                        │  Checkpoint │
                        └──────┬──────┘
                               │
                               │ (Checkpoints)
                               │
                        ┌──────▼──────┐
                        │     NN      │
                        │  NameNode   │
                        │  (Master)   │
                        │             │
                        │ • Metadata  │
                        │ • Namespace │
                        │ • Block map │
                        └──────┬──────┘
                               │
            ┌──────────────────┼──────────────────┐
            │                  │                  │
            ▼                  ▼                  ▼
      ┌──────────┐       ┌──────────┐       ┌──────────┐
      │   DN 1   │       │   DN 2   │       │   DN 3   │
      │ DataNode │       │ DataNode │       │ DataNode │
      │ (Slave)  │       │ (Slave)  │       │ (Slave)  │
      │          │       │          │       │          │
      │ Block A  │       │ Block A  │       │ Block B  │
      │ Block B  │       │ Block C  │       │ Block C  │
      │          │       │          │       │          │
      └──────────┘       └──────────┘       └──────────┘
      
      (And many more DataNodes...)
```


## Components

|**Component**|**Role**|
|---|---|
|**NameNode (NN)**|The master. Manages the metadata about files, directories and blocks (which blocks make up a file and which DataNodes hold them). The metadata is loaded in RAM.|
|**DataNode (DN)**|The slaves. Store the actual data blocks and handle read/write operations. They send **heartbeats** and **block reports** to the NameNode so it knows they are alive and what they hold.|
|**Secondary NameNode (SNN)**|Added because the NameNode is a **single point of failure (SPOF)**. According to the slides, it monitors the NN, copies its metadata and replaces it in case of failure.|

### Data blocks

A **block** is the smallest unit of data storage in HDFS.

|Parameter|Default Value|Description|
|---|---|---|
|**Block Size**|128 MB|Files are split into 128 MB chunks|
|**Replication Factor**|3|Each block stored 3 times|
**Data block example**

```text
File: mydata.txt (550 MB)
Block Size: 128 MB

┌─────────────────────────────────────────┐
│           FILE SPLITTING                │
├─────────────────────────────────────────┤
│                                         │
│  mydata.txt (550 MB)                    │
│                                         │
│  Split into 5 blocks:                   │
│  ┌─────────┐ ┌─────────┐ ┌─────────┐   │
│  │ Block 1 │ │ Block 2 │ │ Block 3 │   │
│  │ 128 MB  │ │ 128 MB  │ │ 128 MB  │   │
│  └─────────┘ └─────────┘ └─────────┘   │
│  ┌─────────┐ ┌─────────┐               │
│  │ Block 4 │ │ Block 5 │               │
│  │ 128 MB  │ │ 38 MB   │ ← Partial     │
│  └─────────┘ └─────────┘               │
│                                         │
│  Total: 5 blocks (4 full + 1 partial)   │
│                                         │
└─────────────────────────────────────────┘
```

**NameNode example***

```text
NameNode Memory (RAM):
┌─────────────────────────────────────┐
│  FILE SYSTEM NAMESPACE              │
├─────────────────────────────────────┤
│  /user/data/file.txt                │
│    ├── Block A: DN1, DN3, DN5       │
│    ├── Block B: DN2, DN4, DN6       │
│    └── Block C: DN1, DN2, DN7       │
│                                     │
│  /user/logs/access.log              │
│    ├── Block D: DN2, DN5, DN8       │
│    └── Block E: DN3, DN6, DN9       │
│                                     │
│  (File → Block → DataNode mapping)  │
└─────────────────────────────────────┘
```

**DataNode example**

```text
DataNode 1 (DN1) Disk:
┌─────────────────────────────────────┐
│  blocks/                            │
│    ├── blk_A (128 MB)               │
│    ├── blk_B (128 MB)               │
│    ├── blk_F (45 MB) ← Last block   │
│    └── ...                          │
└─────────────────────────────────────┘

DataNode 2 (DN2) Disk:
┌─────────────────────────────────────┐
│  blocks/                            │
│    ├── blk_B (128 MB)               │
│    ├── blk_C (128 MB)               │
│    └── ...                          │
└─────────────────────────────────────┘

Every 3 seconds (Heartbeat):
┌──────────┐                    ┌──────────┐
│ DataNode │ ─────────────────► │ NameNode │
│          │  "I'm alive!"      │          │
└──────────┘                    └──────────┘

Every 6 hours (Block Report):
┌──────────┐                    ┌──────────┐
│ DataNode │ ─────────────────► │ NameNode │
│          │  "I have blocks:   │          │
│          │   A, B, F"         │          │
└──────────┘                    └──────────┘
```


# Example

![[image-421.png]]