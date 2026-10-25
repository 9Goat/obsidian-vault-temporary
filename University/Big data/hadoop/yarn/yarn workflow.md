```text
┌─────────────────────────────────────────────────────────────┐
│           CORRECTED YARN FLOW                               │
└─────────────────────────────────────────────────────────────┘

Step 1: Client submits application to ResourceManager
        │
        ▼
Step 2: ResourceManager finds a NodeManager with resources
        │
        ▼
Step 3: ResourceManager asks NodeManager to create container
        │
        ▼
Step 4: NodeManager creates container and starts ApplicationMaster
        │
        ▼
Step 5: ApplicationMaster registers with ResourceManager
        │
        ▼
Step 6: ApplicationMaster requests resources from ResourceManager
        │
        ▼
Step 7: ResourceManager tells other NodeManagers to create containers
        │
        ▼
Step 8: ApplicationMaster tells tasks to run in those containers
        │
        ▼
Step 9: Tasks report to ApplicationMaster
        │
        ▼
Step 10: ApplicationMaster reports job status to ResourceManager
```


![[image-428.png]]