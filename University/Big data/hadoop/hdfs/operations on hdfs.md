
# Read operation

|Step|Action|Description|
|---|---|---|
|**1**|**Open Request**|Client asks NameNode to open file|
|**2**|**Get Locations**|NameNode returns list of DataNodes for each block, sorted by proximity|
|**3**|**Read Block**|Client connects to closest DataNode and reads block|
|**4**|**Failover**|If DataNode fails, client tries next DataNode in list|
|**5**|**Repeat**|Process repeats for all blocks in file|

![[image-423.png]]
## Example

```text
┌─────────────────────────────────────────────────────────────┐
│              HDFS READ OPERATION                            │
└─────────────────────────────────────────────────────────────┘

Step 1: Client requests read
┌────────┐                    ┌──────────┐
│ Client │ ─────────────────► │ NameNode │
│        │ "Read /file.txt"   │          │
└────────┘                    └──────────┘

Step 2: NameNode returns block locations
┌────────┐                    ┌──────────┐
│ Client │ ◄───────────────── │ NameNode │
│        │ "Block A: DN1,    │          │
│        │  DN3, DN5         │          │
│        │  (sorted by       │          │
│        │   proximity)"     │          │
└────────┘                    └──────────┘

Step 3: Client reads from closest DataNode
┌────────┐      ┌─────┐
│ Client │◄─────│ DN1 │
│        │ Read │Blk A│
└────────┘      └─────┘
   (If DN1 fails, try DN3, then DN5)

Step 4: Repeat for all blocks
┌────────┐      ┌─────┐
│ Client │◄─────│ DN3 │
│        │ Read │Blk B│
└────────┘      └─────┘
```


# Write operation

|Step|Action|Description|
|---|---|---|
|**1**|**Create Request**|Client asks NameNode to create file|
|**2**|**Block Allocation**|NameNode creates file in namespace, calculates block topology, returns list of DataNodes|
|**3**|**Write Pipeline**|Client sends data to first DN, which forwards to next DN, forming a pipeline|
|**4**|**Acknowledgment**|Each DN sends ACK back through pipeline to confirm successful write|
|**5**|**Completion**|Client notifies NameNode; NameNode updates metadata|

![[image-424.png]]
## Example


```text
┌─────────────────────────────────────────────────────────────┐
│              HDFS WRITE OPERATION                           │
└─────────────────────────────────────────────────────────────┘

Step 1: Client requests write
┌────────┐                    ┌──────────┐
│ Client │ ─────────────────► │ NameNode │
│        │ "Write /file.txt"  │          │
└────────┘                    └──────────┘

Step 2: NameNode responds with DataNode list
┌────────┐                    ┌──────────┐
│ Client │ ◄───────────────── │ NameNode │
│        │ "Write to:         │          │
│        │  DN1, DN3, DN5"    │          │
└────────┘                    └──────────┘
         (Pipeline: DN1 → DN3 → DN5)

Step 3: Client writes to first DataNode (Pipeline)
┌────────┐      ┌─────┐      ┌─────┐      ┌─────┐
│ Client │─────►│ DN1 │─────►│ DN3 │─────►│ DN5 │
│        │      │Blk A│      │Blk A│      │Blk A│
└────────┘      └─────┘      └─────┘      └─────┘
   (Data flows through the pipeline)

Step 4: Acknowledgments flow back
┌────────┐      ┌─────┐      ┌─────┐      ┌─────┐
│ Client │◄─────│ DN1 │◄─────│ DN3 │◄─────│ DN5 │
│        │ ACK  │     │ ACK  │     │ ACK  │     │
└────────┘      └─────┘      └─────┘      └─────┘

Step 5: Client notifies NameNode of completion
┌────────┐                    ┌──────────┐
│ Client │ ─────────────────► │ NameNode │
│        │ "Write complete"   │          │
└────────┘                    └──────────┘
```

# Replication operation

A cluster is organized in **racks** (groups of machines sharing a network switch). HDFS places replicas so that the data survives both a node failure and a whole-rack failure, while keeping network traffic reasonable.

- **1st copy:** on the local DataNode.
- **2nd copy:** on another DataNode of the same rack (as described in the slides).
- **3rd copy:** on a DataNode in a different rack.
- **For additional copies**: never two copies on the same DataNode; no more than two copies in the same rack; the number of racks used must be lower than the number of copies.

![[image-425.png]]

## Example

```text
┌─────────────────────────────────────────────────────────────┐
│              BLOCK A PLACEMENT (RF=5)                       │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Step 1: 1st Copy - LOCAL NODE                              │
│  ┌─────────────────────────────────────────┐                │
│  │ Client is on DN1 → Place on DN1         │                │
│  │ Location: DN1 (Rack 1)                  │                │
│  │ Reason: Fast write, no network traffic  │                │
│  └─────────────────────────────────────────┘                │
│                                                             │
│  Step 2: 2nd Copy - SAME RACK, DIFFERENT NODE               │
│  ┌─────────────────────────────────────────┐                │
│  │ Rack 1 has DN1, DN2, DN3                │                │
│  │ DN1 is taken → Choose DN2               │                │
│  │ Location: DN2 (Rack 1)                  │                │
│  │ Reason: High bandwidth within rack      │                │
│  └─────────────────────────────────────────┘                │
│                                                             │
│  Step 3: 3rd Copy - DIFFERENT RACK                          │
│  ┌─────────────────────────────────────────┐                │
│  │ Must be on Rack 2 or Rack 3             │                │
│  │ Choose DN4                              │                │
│  │ Location: DN4 (Rack 2)                  │                │
│  │ Reason: Protect against rack failure    │                │
│  └─────────────────────────────────────────┘                │
│                                                             │
│  Step 4: 4th Copy - RANDOM (respecting constraints)         │
│  ┌─────────────────────────────────────────┐                │
│  │ Current: Rack 1 has 2 copies (MAX!)     │                │
│  │          Rack 2 has 1 copy              │                │
│  │          Rack 3 has 0 copies            │                │
│  │                                         │                │
│  │ Can place on: Rack 2 or Rack 3          │                │
│  │ Choose DN5 (Rack 2)                     │                │
│  │ Location: DN5 (Rack 2)                  │                │
│  └─────────────────────────────────────────┘                │
│                                                             │
│  Step 5: 5th Copy - RANDOM (respecting constraints)         │
│  ┌─────────────────────────────────────────┐                │
│  │ Current: Rack 1 has 2 copies (MAX!)     │                │
│  │          Rack 2 has 2 copies (MAX!)     │                │
│  │          Rack 3 has 0 copies            │                │
│  │                                         │                │
│  │ MUST place on Rack 3                    │                │
│  │ Choose DN7                              │                │
│  │ Location: DN7 (Rack 3)                  │                │
│  └─────────────────────────────────────────┘                │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

## Replication with erasure coding

Erasure Coding is a data protection method that reduces storage overhead by using parity blocks instead of full data replication.

|Point|Description|
|---|---|
|**Inspired by**|RAID technology (Redundant Array of Independent Disks)|
|**Replaces**|Full block replication|
|**Benefit**|Reduces data volume by **+50%**|
|**Method**|For 2 data blocks, calculate 1 parity block|

### Problem with current replication system

```text
┌─────────────────────────────────────────────────────────────┐
│           TRADITIONAL REPLICATION (RF=3)                    │
└─────────────────────────────────────────────────────────────┘

Original File: 1 GB (divided into 6 blocks of ~170 MB each)

Block 1: Copied 3 times = 3 × 170 MB = 510 MB
Block 2: Copied 3 times = 3 × 170 MB = 510 MB
Block 3: Copied 3 times = 3 × 170 MB = 510 MB
Block 4: Copied 3 times = 3 × 170 MB = 510 MB
Block 5: Copied 3 times = 3 × 170 MB = 510 MB
Block 6: Copied 3 times = 3 × 170 MB = 510 MB

Total Storage: 3 GB (for 1 GB of actual data)
Storage Overhead: 200% (3x the original size)
```

|Aspect|Problem|
|---|---|
|**Storage Cost**|3x storage needed|
|**Network Traffic**|3x data transfer during write|
|**Efficiency**|Only 33% storage efficiency|

### How erasure coding works

```text
┌─────────────────────────────────────────────────────────────┐
│              ERASURE CODING (Simple Example)                │
└─────────────────────────────────────────────────────────────┘

Original Data: 2 blocks

┌─────────────┐  ┌─────────────┐
│  Data Block │  │  Data Block │
│     A       │  │     B       │
│   (100 MB)  │  │   (100 MB)  │
└──────┬──────┘  └──────┬──────┘
       │                │
       └────────┬───────┘
                │
                ▼
       ┌─────────────────┐
       │  Calculate XOR  │
       │   A ⊕ B = P     │
       └────────┬────────┘
                │
                ▼
       ┌─────────────────┐
       │  Parity Block   │
       │       P         │
       │    (100 MB)     │
       └─────────────────┘

Total Storage: 300 MB (for 200 MB of data)
Storage Overhead: 50% (instead of 200% with RF=3!)
```

|A|B|A XOR B (P)|
|---|---|---|
|0|0|0|
|0|1|1|
|1|0|1|
|1|1|0|

###  Example

```text
Block A: H  E  L
         72 69 76  (ASCII values in binary)

Block B: L  O  _
         76 79 0   (padded with 0)

Parity P = A XOR B

H XOR L = 72 XOR 76 = 12
E XOR O = 69 XOR 79 = 14
L XOR _ = 76 XOR 0  = 76

Parity Block P: 12  14  76

┌─────────────┐  ┌─────────────┐  ┌─────────────┐
│  Block A    │  │  Block B    │  │  Parity P   │
│  "HEL"      │  │  "LO"       │  │  12 14 76   │
│  72 69 76   │  │  76 79 0    │  │             │
└─────────────┘  └─────────────┘  └─────────────┘

Total storage: 3 blocks (instead of 4 with RF=2)
```


```text
BEFORE LOSS:
┌─────────────┐  ┌─────────────┐  ┌─────────────┐
│  Block A    │  │  Block B    │  │  Parity P   │
│  "HEL"      │  │  "LO"       │  │  12 14 76   │
│  72 69 76   │  │  76 79 0    │  │             │
└─────────────┘  └─────────────┘  └─────────────┘

AFTER LOSS:
┌─────────────┐  ┌─────────────┐  ┌─────────────┐
│  Block A    │  │  Block B    │  │  Parity P   │
│  ❌ LOST!   │  │  "LO"       │  │  12 14 76   │
│             │  │  76 79 0    │  │             │
└─────────────┘  └─────────────┘  └─────────────┘

We know:
- Block B = 76 79 0
- Parity P = 12 14 76
- Formula: A = P XOR B

Recovery:
A[0] = P[0] XOR B[0] = 12 XOR 76 = 72 → 'H'
A[1] = P[1] XOR B[1] = 14 XOR 79 = 69 → 'E'
A[2] = P[2] XOR B[2] = 76 XOR 0  = 76 → 'L'

Recovered Block A: 72 69 76 = "HEL" ✅
```

