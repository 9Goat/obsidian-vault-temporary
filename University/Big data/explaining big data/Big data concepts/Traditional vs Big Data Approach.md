#  Introduction

The way organizations handle data has fundamentally changed with Big Data. Let's compare the **traditional approach** (how things were done before) with the **Big Data approach** (how things are done now).

#  Traditional approach

## Step 1: Business Defines the Need

- The business team identifies a specific question or problem
- Example: "We need to know which products are our best sellers"

## Step 2: IT Designs the Solution

- IT team designs a system specifically for that question
- Creates database schema, reports, and queries
- Example: Build a sales reporting system

## Step 3: Data Collection

- Collect **only** the data needed to answer that specific question
- Data is carefully structured and cleaned before storage
- Example: Extract sales data from POS systems

## Step 4: Data Storage

- Store in a **structured database** (SQL)
- Expensive, high-quality storage (SAN - Storage Area Network)
- Data is organized in tables with strict schema

## Step 5: Reporting

- Generate reports to answer the original question
- Business uses reports for decision-making
- Example: Monthly sales report by product

## Characteristic

|Characteristic|Description|
|---|---|
|**Question-driven**|Start with a specific question|
|**Structured only**|Only works with clean, organized data|
|**Sequential**|One step after another, no going back|
|**Expensive storage**|SAN (Storage Area Network) - very costly|
|**Rigid**|Hard to change once built|
|**Limited scope**|Only answers predefined questions|

## Problems with Traditional Approach

1. **Expensive**: SAN storage and enterprise software cost a fortune
2. **Slow**: Takes months to build a solution
3. **Rigid**: Can't easily answer new questions
4. **Limited**: Only works with structured data
5. **Wasteful**: Discards "useless" data that might be valuable later

# Big data approach


## Step 1: Identify All Data Sources

- Business and IT work together to identify **all available data**
- Don't filter yet—collect everything!
- Example: Sales data, website logs, social media, customer emails, sensor data

## Step 2: Store Everything (Data Lake)

- Store **all data** in raw format (structured + unstructured)
- Use cheap, commodity hardware (HDFS)
- Don't worry about structure yet—store first, organize later
- Example: Dump everything into Hadoop/HDFS

## Step 3: Explore & Discover

- Data scientists explore the data to find patterns
- Use tools to analyze raw data
- Discover unexpected insights
- Example: "Interesting—customers who buy X also browse category Y"

## Step 4: Ask Questions

- Business asks new questions based on discoveries
- Questions emerge **from the data**, not before
- Example: "Can we predict which customers will buy X?"

## Step 5: Iterate & Refine

- Try new analyses, learn, and repeat
- New ideas lead to new technologies
- Continuous improvement cycle
- Example: Add machine learning, real-time processing, etc.

## Characteristics

|Characteristic|Description|
|---|---|
|**Data-driven**|Start with data, discover questions|
|**All data types**|Structured, semi-structured, unstructured|
|**Iterative**|Try, learn, repeat—continuous cycle|
|**Cheap storage**|Commodity hardware, distributed systems|
|**Flexible**|Easy to adapt and explore new ideas|
|**Comprehensive**|Can answer questions you didn't think to ask|

## Advantages of Big Data Approach

1. **Cost-effective**: Commodity hardware is cheap
2. **Fast**: Can start analyzing immediately
3. **Flexible**: Easy to answer new questions
4. **Comprehensive**: Works with all data types
5. **Valuable**: Keeps data that might be useful later
6. **Innovative**: Discovers unexpected insights

# Combining both approaches

the following graph show cases the steps and the processes needed to apply both approaches

## Components

![[image-417.png]]


## Generating reports and analytics

![[image-418.png]]


## Generating data for algorithms

![[image-419.png]]


