there are 3 main ways to store data in big data, and it resolves around the way we structure it, which are the followings:

- stuctured
- unstructured
- semi structured

# Structured data

## Definition

**Structured data is data that is organized in a fixed format with a clear structure—typically rows and columns, like a table.**

## Characteristics

- Has a **predefined schema** (structure is decided before data is stored)
- Fits neatly into **tables** with rows and columns
- Each field has a **specific data type** (text, number, date, etc.)
- Easy to **search, sort, and analyze**
- Stored in **relational databases** (SQL databases)

## Real-World Examples

| Example                | Description                                    |
| ---------------------- | ---------------------------------------------- |
| **Excel Spreadsheets** | Student grades, budget sheets                  |
| **SQL Databases**      | Customer records, product inventory            |
| **Bank Transactions**  | Date, amount, account number, transaction type |
| **Employee Database**  | Name, ID, salary, department, hire date        |
# Unstructured data

## Definition

**Unstructured data is data that has no predefined structure or organization. It doesn't fit into traditional row-column formats.**

## Characteristics

- No **predefined schema**
- Cannot be easily organized into tables
- Comes in **many different formats**
- Difficult to **search and analyze** using traditional tools
- Requires **special tools** (like Big Data technologies!)

# Semi structured data

## Definition

**Semi-structured data is data that doesn't fit into a rigid table structure but has some organizational properties (like tags, labels, or keys) that make it easier to analyze than unstructured data.**

## Characteristics

-  Has **some structure** but not a rigid schema
- Contains **tags or markers** to organize elements
-  More flexible than structured data
-  Easier to process than unstructured data
- Schema can **change/evolve** over time

# Summary table

|Feature|Structured|Semi-Structured|Unstructured|
|---|---|---|---|
|**Schema**|Fixed, predefined|Flexible, evolving|No schema|
|**Format**|Tables (rows/columns)|Tags, keys, hierarchies|Free-form|
|**Search**|Easy (SQL queries)|Moderate (parsing needed)|Difficult|
|**Storage**|Relational databases|NoSQL, files|File systems, data lakes|
|**Examples**|Excel, SQL databases|JSON, XML, logs|Videos, images, social media|
|**% of World Data**|~10%|~10-20%|~80-90%|

