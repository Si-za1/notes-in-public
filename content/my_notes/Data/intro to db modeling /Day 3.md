---
title: Day3
draft: false
tags:
  - data
---
## Quick Recap: What We’ve Covered So Far (Day 1 & Day 2)

Before moving forward, let’s briefly recap what we’ve already established.

So far, we have learned how to:

- **Identify entities**  
    Finding the major objects or concepts in a system  
    _(e.g., Customer, Product, Order)_
    
- **Extract business rules**  
    Understanding constraints and conditions the system must always follow  
    _(e.g., “An Order must contain at least one Product”)_
    
- **Define relationships**  
    Identifying how entities interact  
    _(e.g., a Customer places an Order)_
    
- **Create an ER Diagram (ERD)**  
    A visual representation of:
    
    - Entities
        
    - Relationships
        
    - Cardinality & modality
        
    - Notations, tools, and techniques

We did all without having to think about the technical implementation.

## What We’ll Cover Today

Today, we move one step closer to implementation, but still without writing SQL.

### Topics for Day 3

- Logical Data Modeling
    
- Introduction to different types of keys
    
- Introduction to normalization
    
- Data anomalies and redundancy
    
- Why normalization became necessary

So, let's get started. 

## From Conceptual to Logical Modeling

So far, conceptual modeling helped us answer:

> **What data exists, and how is it related?**

Logical modeling answers the next question:

> **How should this data be structured logically so it stays correct, consistent, and scalable?**

If conceptual modeling was about creating the **blueprint**,  
logical modeling is about **making that blueprint precise and usable**.

## What Happens in Logical Data Modeling?

At this stage, we take our conceptual ER model and refine it.

### Key Activities in Logical Modeling

- **Define attributes in detail**  
    Specify attributes more precisely  
    (e.g., Customer Name, Product Price)
    
- **Apply normalization**  
    Organize data to:
    
    - Reduce redundancy
        
    - Improve data integrity
        
- **Define primary keys**  
    Identify unique identifiers for each entity  
    (e.g., Student ID, Order ID)
    
- **Define foreign keys**  
    Establish relationships between entities  
    (e.g., Customer ID in Order table)
    
- **Ensure integrity constraints**
    
    - Not null
        
    - Unique
        
    - Referential integrity
        

At this point, our model becomes:

- Structured
    
- Unambiguous
    
- Ready for database implementation

## Introduction to Keys

Keys are fundamental in logical modeling because they help us answer:

- How do we uniquely identify a record?
    
- How do we connect one table to another?


### Types of Keys

We’ll look at the following types of keys:

- Primary Key
    
- Foreign Key
    
- Super Key
    
- Candidate Key
    
- Alternate Key
    
- Surrogate Key
    
- Natural Key
    

Rather than memorizing definitions, let’s understand them **through thinking and examples**.


## Hands-On Exercise: Identifying Different Keys

### Given Relation: `Student`

|std_id|reg_no|name|
|---|---|---|
|1|3435|Ram|
|2|9878|Shyam|
|3|5647|Hari|
|4|9999|Ram|

You are asked to identify **different types of keys** for this relation.

## How I Think Through This Problem

### Step 1: Identify Super Keys

A **super key** is any combination of attributes that can uniquely identify a record.

Looking at the table:

Possible super keys are:

- `{std_id}`
    
- `{reg_no}`
    
- `{std_id, reg_no}`
    
- `{std_id, name}`
    
- `{reg_no, name}`
    
- `{std_id, reg_no, name}`
    

All of these uniquely identify rows.

### Step 2: Identify Candidate Keys

A **candidate key** is a _minimal_ super key, remove anything, and uniqueness breaks.

From the super keys above:

- `{std_id}`
    
- `{reg_no}`
    

These are minimal and still unique.

### Step 3: Select the Primary Key

From the candidate keys, we select **one** to act as the primary key.

Here, we choose:

- `{std_id}` → **Primary Key**
    

Why?

- Stable
    
- Short
    
- Meaningless outside the system (good for performance)
    

### Step 4: Alternate Key

The candidate key that is **not selected** becomes an **alternate key**.

- `{reg_no}` → Alternate Key
    
### Step 5: Natural vs Surrogate Key

- **Natural Key:**  
    Comes from real-world meaning
    
    - Example: `reg_no`
        
- **Surrogate Key:**  
    Artificial, system-generated
    
    - Example: `std_id`
        

In practice, we often:

- Use surrogate keys as primary keys
    
- Enforce natural keys using unique constraints


## Types of Data Anomalies (With Examples)

To understand data anomalies, let’s start with **a sample table**.

### A sample Table: `Student_Course`

|student_id|student_name|course_id|course_name|instructor|
|---|---|---|---|---|
|1|Ram|C101|Databases|Prof. A|
|1|Ram|C102|OS|Prof. B|
|2|Shyam|C101|Databases|Prof. A|
|3|Hari|C103|Networks|Prof. C|

At first glance, this table looks fine.

But this design is **guaranteed to cause problems**.

## Insertion Anomaly

### What it means

> You **cannot insert data** without adding unrelated or incomplete data.

### Example

Suppose:

- A new course **C104 (AI Basics)** is introduced
    
- No students have enrolled yet
    

**Problem:**  
Where do we store this course?

We cannot insert:

- course_id
    
- course_name
    
- instructor
    
**without also inserting student data**, because this table _forces_ student information.

Result:

- We cannot store valid course information independently
    
## Update Anomaly

### What it means

> The **same data appears in multiple rows**, and must be updated everywhere.

### Example

Let’s say:

- Prof. A changes their name to **Prof. A Sharma**
    

Now look at the table:

- Prof. A appears in **multiple rows** for course `C101`
    

We must update **every row** where:

- course_id = C101
    

 If we miss even one row:

- The database becomes **inconsistent**
    
- Same course has different instructor names
    
## Deletion Anomaly

### What it means

> Deleting one record **removes important data unintentionally**.

### Example

Suppose:

- Student Hari (student_id = 3) drops out
    
We delete this row:

| 3 | Hari | C103 | Networks | Prof. C |

**Problem:**  
Now we have lost:

- Information about course **Networks**
    
- Information about **Prof. C**
    

Even though:

- The course still exists
    
- The instructor still exists
    

Important business data is gone.

## Why These Problems Occur

All three anomalies happen because:

- Multiple concepts are mixed in one table
    
- Data is repeated
    
- There is no clear separation of responsibility
    
This is **exactly why normalization exists**.

## Key Takeaway

> **Data anomalies are symptoms.  
> Poor design is the disease.**

Normalization doesn’t make databases complex, it makes them **correct, stable, and scalable**.

