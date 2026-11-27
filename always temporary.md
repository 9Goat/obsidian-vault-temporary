
Here is the full improved set. Everything inside the code blocks is copy-paste ready, and you replace `<NUMBER>` and `<RANGE>` yourself.

## Before you start (checklist)

```text
1. Created the Android Studio Empty Activity project at mobile-compose/ (package com.mindspark.compose, Kotlin DSL) and let Gradle sync once.
2. Saved docs/mobile-compose/IMPLEMENTATION_PLAN.md and docs/mobile-compose/AGENT_WORKFLOW.md.
3. Completed Task 0 and added hostIp=<your LAN IP> to ~/.gradle/gradle.properties.
4. Opened Antigravity at the monorepo ROOT (not inside mobile-compose/).
5. Phone connected with USB debugging authorised; backend + Keycloak running.
6. JAVA_HOME works in the terminal; git working tree is clean.
```

Start a fresh Antigravity chat for every task below.

## Prompt 1: Task 1 (first chat)

```text
You are building the MindSpark Jetpack Compose Android client in `mobile-compose/` inside this monorepo.

Read `docs/mobile-compose/AGENT_WORKFLOW.md` first. Then, from `docs/mobile-compose/IMPLEMENTATION_PLAN.md`, read ONLY: Code Level Rules (Units 1-5), Global Constraints, Compose and Android traps, Execution notes, and Task 1.

Context:
- I already created the Android Studio Empty Activity project at `mobile-compose/` and completed Task 0. Do NOT recreate the project; configure the existing one.
- `docs/mobile-compose/contracts.md` does not exist yet (Task 2 creates it).
- In `app/build.gradle.kts`, read the host IP with `project.findProperty("hostIp")?.toString()?.trim()` so it works both from `~/.gradle/gradle.properties` and from `-PhostIp=...`.

Follow Tier A from AGENT_WORKFLOW.md:
1. Write the failing tests specified in Task 1 first, run `./gradlew testDebugUnitTest`, and confirm they FAIL.
2. Implement `EnvConfig` (pure JVM: `java.net.URLEncoder`, no `android.*` APIs) and the theme using basic Units 1-5 code only.
3. Run `./gradlew testDebugUnitTest` and `./gradlew assembleDebug` from `mobile-compose/` and show the test summary, the BUILD SUCCESSFUL lines, and the dependency versions you chose.
4. Task 1 ends with a Checkpoint: list exactly what I should verify on my phone, then STOP. Do not commit until I confirm it works.
```

## Task 2: contracts (Tier B, special case)

```text
Read `docs/mobile-compose/AGENT_WORKFLOW.md`, and from `docs/mobile-compose/IMPLEMENTATION_PLAN.md` read the header rules/traps plus Task 2 only. `contracts.md` does not exist yet; you are creating it in this task.

Follow Tier B: read the backend and Angular sources listed in Task 2, then output ONLY a short Pre-Code Check (source rules, differences vs Appendix A so far, file list) and wait for my "Go". Use real JSON copied from backend tests or captured with curl and a token; do not invent fields.

After my "Go": write `contracts.md` and the fixtures, run `FixturesTest`, report any differences vs Appendix A, and STOP for my verification before Task 3.
```

## Complex tasks: 3, 9, 10, 13, 14, 16, 17 (Tier B)

```text
Read `docs/mobile-compose/AGENT_WORKFLOW.md`, `docs/mobile-compose/contracts.md`, and from `docs/mobile-compose/IMPLEMENTATION_PLAN.md` read the header rules/traps plus Task <NUMBER> only.

We are starting Task <NUMBER>. Follow Tier B: read the relevant source/contract files first and output ONLY your short Pre-Code Check (source rules with quoted numbers, trap/gesture check, file list). Wait for my approval ("Go") before writing any tests or code.

After my approval, follow the TDD loop, run `./gradlew testDebugUnitTest` and `./gradlew assembleDebug`, and show the output. If the task ends with a Checkpoint or needs `connectedDebugAndroidTest`, tell me exactly what to run or test and STOP; commit only after I confirm.
```

## Standard tasks: 4, 5, 6, 7, 8, 11, 12, 15, 18 (Tier A)

```text
Read `docs/mobile-compose/AGENT_WORKFLOW.md`, `docs/mobile-compose/contracts.md`, and from `docs/mobile-compose/IMPLEMENTATION_PLAN.md` read the header rules/traps plus Task <NUMBER> only (and any source file the task names).

Implement Task <NUMBER> strictly following Tier A: write the failing tests first and confirm they fail, then implement with Units 1-5 basic Kotlin/Compose only, obeying all Compose/Android traps.

Run `./gradlew testDebugUnitTest` and `./gradlew assembleDebug` and show the output. If the task ends with a Checkpoint or needs `connectedDebugAndroidTest`, tell me exactly what to run or test and STOP; commit only after I confirm.
```

## Milestone reviews (fresh chat, read-only)

Use these ranges: after Task 5 → `1-5`, after 10 → `6-10`, after 13 → `11-13`, after 17 → `14-17`.

```text
Read `docs/mobile-compose/AGENT_WORKFLOW.md` and the Code Level Rules + Compose and Android traps in `docs/mobile-compose/IMPLEMENTATION_PLAN.md`.

Review the Kotlin code in `mobile-compose/app/src/main/` written for Tasks <RANGE>.

This is a READ-ONLY review: do NOT modify any files. Give me a numbered list of findings, each with file, line and a one-line fix suggestion. List ONLY real bugs, violations of Units 1-5 rules (forbidden Flow operators, missing factories/keys, wrong coordinate scaling, gesture/coroutine leaks, two `detect*Gestures` in one `pointerInput`), or missing edge cases. No style rewrites or advanced patterns.
```


### 1. How to Detect Which Source Tables You Need

- **Work backwards from the Target Table (page 5):**
    
    1. List every target column and find which source table (page 4) holds it.
        
    2. Add **bridge tables** only if needed to connect a key to a required column (e.g., `Country` in `Geography_Dim` is needed to reach `Continent`).
        
    3. Ignore dead-end tables (`Geo_Type`, `Price_List`, `Discount`) and redundant tables whose columns already exist on your main table (`City`, `Postal_Code`).
        
- **Don't read `*_Dim` tables to build `Order_Fact`:** Operational IDs in `orion.mdb` already match the dimension IDs. You only read `*_Dim` tables if you are building the filtered **Datamart** (page 13).
    

### 2. Self-Referencing Hierarchies (How Many Copies?)

- **Spot the loop:** If a source table has an arrow pointing **back to itself** (`Product_List.Product_Ref_ID`, `Organization.Org_Ref_ID`), you need **1 `tDBInput` copy per hierarchy level** shown in the target table (`4` for `Product_Dim`, `5` for `Organization_Dim`).
    
- **Find the level numbers first:** Run `SELECT * FROM Product_Level` / `Org_Level` (or `SELECT Org_Level, COUNT(*) FROM Organization GROUP BY Org_Level`) via **Edit queries**. Largest count = bottom level (Products/Employees); smallest count = top level (Lines/Companies).
    
- **Filter each copy:** In each `tDBInput` → **Guess Query** → add `WHERE <Level_Col> = <num>` **inside** the double quotes `"..."` with **no semicolon `;`**.
    

## 3. Choosing `Main` vs. `Lookup` in `tMap`

- **Simple rule:** **`Main`** is the table that has **one row for each row you want in your final target table** (the main "subject" of the job). **`Lookup`** tables are everything else—they just add extra details to each `Main` row.
    
    - Building `Customer_Dim` (1 row per customer)? → **`Customer`** is `Main`.
        
    - Building `Product_Dim` (1 row per product)? → **`Product_List` (Product level)** is `Main` _(never Product Line, or you'd only get 4 rows)_.
        
    - Building `Organization_Dim` (1 row per employee)? → **`Staff`** (`staff.xls`) is `Main` _(never Company or Department)_.
        
    - Building `Geography_Dim` (1 row per street)? → **`Street_Code`** is `Main` _(never Country or Continent)_.
        
    - Building `Order_Fact` (1 row per item bought)? → **`Order_Item`** is `Main` _(never `Orders`, because one order can have multiple items)_.
        
- **Never leave `Expr. key` empty** on a Lookup—an empty key creates a huge cross-join and duplicate primary key errors.
    

### 4. `tMap` Join & Expression Traps

- **Left Outer Join vs. Inner Join:** Leave **Inner join unchecked** for optional parent levels like `County` and `State` in `Geography_Dim` (otherwise countries without states get dropped). Check **Inner join** only when intentionally filtering (like the Datamart on page 13).
    
- **Match Model:** Always verify lookups are set to **`Unique match`**.
    
- **Null Dates (`staff.xls`):** Wrap `TalendDate.parseDate(...)` on nullable dates (`Emp_Term_Date`) to avoid `NullPointerException`:
    
    Java
    
    ```
    (row1.Emp_Term_Date == null || row1.Emp_Term_Date.trim().isEmpty())
      ? null
      : TalendDate.parseDate("dd/MM/yyyy", row1.Emp_Term_Date)
    ```
    

### 5. Data Types & Component Rules

- **Keep Access `tDBInput` types simple (page 7):** Use only **`Double`**, **`String`**, and **`Date`** (`DATETIME` → `Date`). Never change an Access `Double` ID to `Integer` inside `tDBInput`.
    
- **Large IDs (`Street_ID`, `Order_ID`):** Avoid `.intValue()` if IDs can exceed 2.14 billion (it clamps them all to `2147483647` and causes duplicate PK errors)—use **`Double`** or **`Long`**.
    
- **Output & Polish (pages 9–10):**
    
    - `tDBOutput`: Set **Action on table** to **Clear table**.
        
    - Add a **Misc / Note** component describing the job.
        
    - Enable **Statistics** in the **Run** tab and verify the row count in SQL afterward.

### Step 1: Set Up & Check Schemas (First 3 Minutes)

- [ ] **Create the target table** in your warehouse DB (in MySQL, use `BIGINT` for large IDs like `Product_ID`, `Street_ID`, `Order_ID`).
    
- [ ] **Retrieve/Refresh Schemas** in Talend (`orion_BD`, `staff`, `orion_DW`).
    
- [ ] **Check types:** Keep all Access/Excel numbers as **`Double`**, text as **`String`**, and `DATETIME` as **`Date`**.
    
- [ ] **Verify source columns:** If anything looks missing, right-click the table → **Edit queries** → `SELECT * FROM <table>` (click **Cancel** when done).
    

### Step 2: Plan the Job Before Dragging Components (2 Minutes)

- [ ] **Work backwards from the target columns:** Identify every source table needed (+ any bridge table like `Country` for `Continent`).
    
- [ ] **Check for self-referencing loops** (`Product_List`, `Organization`):
    
    - Run `SELECT * FROM Product_Level` / `Org_Level` or `SELECT <Level_Col>, COUNT(*) FROM <table> GROUP BY <Level_Col>` in **Edit queries**.
        
    - Largest count = bottom level (`Product` / `Employee`); smallest count = top level (`Product_Line` / `Company`).
        
- [ ] **Pick your `Main` table** (1 row per target row: `Product`, `Staff`, `Street_Code`, `Order_Item`).
    

### Step 3: Build the Job Skeleton (3 Minutes)

- [ ] Drag your **`Main`** input first, then all **`Lookup`** inputs (1 copy per hierarchy level if self-referencing).
    
- [ ] Add **`tMap`**, **`tDBOutput`** (target table), and a **`Misc / Note`** component.
    
- [ ] **Connect & rename links** (`Main` first, then `Lookups`, then `tMap` → `tDBOutput`) using slow double-click or **`F2`**.
    
- [ ] **Add `WHERE` filters (if needed):** In `tDBInput` → **Guess Query** → add `WHERE <Level_Col> = <num>` **inside** `"..."` with **no `;`**.
    

### Step 4: Configure `tMap` & `tDBOutput` (5 Minutes)

- [ ] **Check lookup order:** Any lookup referenced by another lookup must sit **above** it (use `↑` / `↓` in `tMap`'s top-left toolbar).
    
- [ ] **Set `Expr. key` on every lookup** (never leave an `Expr. key` empty!).
    
- [ ] **Set Match Model** to **`Unique match`** on all lookups.
    
- [ ] **Check Join Model:**
    
    - Leave **Inner join unchecked** for optional parents (`County`, `State`).
        
    - Check **Inner join** for required FKs (`Orders`, `Customer` in `Order_Fact`) or Datamart filters.
        
- [ ] **Guard against nulls & type errors:**
    
    - Wrap nullable dates in `tMap`: `col == null || col.trim().isEmpty() ? null : TalendDate.parseDate(...)`.
        
    - Match output types to `Double` / `Long` (avoid `.intValue()` on large IDs).
        
- [ ] **In `tDBOutput`:** Set **Action on table** to **Clear table**.
    

### Step 5: Run & Verify (Final 2 Minutes)

- [ ] In the **Run** tab, check **Statistics** and press **F6**.
    
- [ ] **Check the green row counts** on the canvas (`Main` rows ≈ `Output` rows—make sure you didn't get 4 rows when you expected 5,500, or 1.5M rows from a missing key).
    
- [ ] **Verify in SQL:** Run `SELECT COUNT(*) FROM <Target_Table>;` and inspect the first 10 rows.