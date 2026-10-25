**MapReduce** is the **processing layer** of Hadoop. It's a programming model that allows you to process massive datasets in parallel across a cluster of computers.

![[image-427.png]]
  
|**Parallel computing**|**Distributed computing**|
|---|---|---|
|**Execution**|Simultaneous threads on one machine|Autonomous nodes|
|**Communication**|Shared memory, which requires synchronization|Message exchange|
|**Scaling**|Vertical (a bigger machine)|Horizontal (more machines)|
|**Weakness / strength**|SPOF: a vulnerable single point of failure|Fault tolerance|

  
MapReduce is an **algorithmic programming model** based on “divide and conquer”: break the problem into independent, parallelizable tasks, and combine two functions, **Map** and **Reduce**.

