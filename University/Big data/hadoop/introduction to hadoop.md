

# Introduction to distributed system
## Definition of distributed system

Hadoop is a distributed system. The slides define it as a collection of independent, cooperating processes or computers that appear to the user as a single, coherent system.

## Benefits of distributed system

 
| **Goal**            | **Meaning**                                                                                                                                                     |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Heterogeneity**   | Machines with different architectures and protocols can work together.                                                                                          |
| **Scalability**     | The system stays efficient when resources and users grow. **Vertical scaling** means using a bigger machine. **Horizontal scaling** means adding more machines. |
| **Fault tolerance** | The service remains available even under degraded conditions, such as when a machine fails.                                                                     |
| **Concurrency**     | Several users or processes can access shared resources at the same time.                                                                                        |
| **Transparency**    | The user sees and uses the whole system as one single entity.                                                                                                   |

##  Limits of distributed system

- Not suited to **low-latency** systems: it is designed for throughput on large scans.
- **Slow with many small files**: every file and block costs NameNode memory and metadata operations.
- Suited to **append-only** usage; random modification of existing data is not supported.
- **Everything is in memory** on the NameNode, which creates a scalability limit.

# benefits of hadoop


- **Linear scalability** in both size and time: doubling the machines roughly doubles capacity or halves the processing time.
- **Availability**, thanks to data replication.
- **Code moves to the data**: computation is sent to the nodes that already hold the data, instead of moving huge volumes across the network (data locality).
- **Sequential access** rather than random access, which suits large scans of data on disk.
- **A simple processing model**: the developer only writes a map and a reduce function.

