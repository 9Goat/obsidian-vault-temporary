**YARN** is the **resource management layer** of Hadoop. It manages cluster resources and schedules jobs. Introduced in **Hadoop 2.0** to solve limitations of Hadoop 1.0.

there are 3 main components of a yarn job scheduler which are:

- resources manager **RM**
- application master **AM**
- node manager **NM**

![[image-429.png]]

# Resources manager

manages resources to applications by communicating with node managers and application master

```text
✅ DOES:
   • Decide WHERE containers are created
   • Allocate resources to applications
   • Monitor NodeManager health
   • Restart failed ApplicationMasters
   
   ❌ DOES NOT:
   • Create containers itself (tells NodeManager to do it)
   • Run application code
   • Monitor individual tasks (that's ApplicationMaster's job)
   • Store application data
```

# Node manager

Creates containers and allocates resources on its node; reports node status to the RM.

```text
✅ DOES:
   • Create containers (when RM instructs)
   • Launch ApplicationMaster (in first container)
   • Launch task containers (when AM instructs)
   • Monitor container resource usage
   • Report node status to ResourceManager
   • Manage local storage
   
   ❌ DOES NOT:
   • Decide which applications run (that's RM's job)
   • Allocate resources globally (only manages its own node)
   • Monitor application progress (that's AM's job)
   • Make scheduling decisions
   • Communicate with other NodeManagers
```

# Application master

Negotiates containers from the RM for the tasks of its application and supervises them.

```text
✅ DOES:
   • Register with ResourceManager
   • Request containers from ResourceManager
   • Coordinate task execution
   • Monitor task progress
   • Handle task failures
   • Report job status
   • Manage application lifecycle
   
   ❌ DOES NOT:
   • Create containers itself (asks RM, which tells NM)
   • Manage other applications (one AM per application)
   • Control cluster-wide resources
   • Run on multiple nodes (runs in ONE container)
   • Make global scheduling decisions
```

# Summary

|Aspect|ResourceManager|NodeManager|ApplicationMaster|
|---|---|---|---|
|**Scope**|Entire cluster|Single node|Single application|
|**Quantity**|1 per cluster (2 in HA)|1 per node|1 per application|
|**Role**|Global scheduler|Node agent|Job coordinator|
|**Manages**|All resources|Local resources|Application tasks|
|**Creates**|Nothing (decides)|Containers|Nothing (coordinates)|
|**Monitors**|NodeManagers, AMs|Containers|Tasks|
|**Reports to**|N/A (top level)|ResourceManager|ResourceManager|
|**Receives from**|Clients, NMs, AMs|ResourceManager, AM|ResourceManager, tasks|
|**Failure impact**|Cluster down (if no HA)|Node unavailable|Application fails|
|**Restarted by**|N/A|Automatic (rejoins cluster)|ResourceManager|
|**Lifetime**|Cluster lifetime|Node lifetime|Application lifetime|

| Task                          | RM  | NM  | AM               |
| ----------------------------- | --- | --- | ---------------- |
| **Receive job submission**    | ✅   | ❌   | ❌                |
| **Decide which node runs AM** | ✅   | ❌   | ❌                |
| **Create AM container**       | ❌   | ✅   | ❌                |
| **Launch ApplicationMaster**  | ❌   | ✅   | ❌                |
| **Register application**      | ✅   | ❌   | ✅                |
| **Request task resources**    | ❌   | ❌   | ✅                |
| **Allocate task containers**  | ✅   | ❌   | ❌                |
| **Create task containers**    | ❌   | ✅   | ❌                |
| **Launch tasks**              | ❌   | ✅   | ✅ (instructs NM) |
| **Monitor task progress**     | ❌   | ❌   | ✅                |
| **Handle task failure**       | ❌   | ❌   | ✅                |
| **Monitor node health**       | ✅   | ❌   | ❌                |
| **Report job status**         | ✅   | ❌   | ✅                |
| **Kill containers**           | ✅   | ✅   | ✅ (via RM)       |
