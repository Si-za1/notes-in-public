---
title: Untitled
draft: false
tags: []
---
 
## Hands-On: Requirement Gathering Exercise

### Scenario: Online Bookstore Management System

You are designing a database for an online bookstore.

#### Stakeholder Inputs

**From Store Owner**

- The store sells books.
    
- Each book has an ISBN and title.
    
- A book can have multiple authors.
    
- Customers can place multiple orders.
    

**From Operations Team**

- We need to store customer name, email, and address.
    
- Each order can contain multiple books.
    
- We want to track order dates.
    

**From IT Team**

- The system should support future features like reviews and ratings.
    
- A customer cannot place an order without at least one book.
    

---

### Your Tasks

1. List the entities
    
2. Identify attributes
    
3. Define relationships and cardinalities
    
4. Extract business rules
    
---
# Solution Walkthrough : My version
## Part 1: Requirement Gathering Exercise

**Scenario: Online Bookstore Management System**

Before jumping to diagrams, I pause and ask myself one question:

> **“What are the nouns in this problem?”**

As, Nouns usually point to **entities**.

---

## Step 1: Listing the Entities (How I Think)

From the stakeholder inputs, I notice repeated mentions of:

- Books
    
- Authors
    
- Customers
    
- Orders
    

These are clear, real-world objects the business cares about.

So, my **initial entity list** becomes:

- **Book**
    
- **Author**
    
- **Customer**
    
- **Order**
    

I don’t overthink this yet. I can always refine later.


## Step 2: Identifying Attributes (How I Think)

Now I ask:

> “What information do we need to store about each entity?”

I only include what is **explicitly mentioned** in the requirements.

### Book

- ISBN
    
- Title
    

### Author

- (No attributes mentioned explicitly yet, but authors exist)
    

### Customer

- Name
    
- Email
    
- Address
    

### Order

- Order Date
    

At this stage, I **don’t invent attributes**.  
If it’s not mentioned or implied, I leave it out.

## Step 3: Defining Relationships & Cardinalities (How I Think)

Now I look for verbs and phrases like:

- _can have_
    
- _can place_
    
- _contains_
    
- _cannot_
    

These usually indicate relationships.

### Book ↔ Author

> “A book can have multiple authors.”

That means:

- One book → many authors
    
- One author → many books
    

**Many-to-Many (M:N)**

---

### Customer ↔ Order

> “Customers can place multiple orders.”

- One customer → many orders
    
- Each order → exactly one customer
    

**One-to-Many (1:M)**

---

### Order ↔ Book

> “Each order can contain multiple books.”

- One order → many books
    
- One book → can appear in many orders
    

**Many-to-Many (M:N)**

---

## Step 4: Extracting Business Rules (How I Think)

At this stage, I stop thinking about tables or diagrams and ask myself:

> **“What statements must ALWAYS be true for this business to function correctly?”**

Business rules usually come from:

- Words like **must**, **cannot**, **only**, **each**, **unique**
    
- Constraints implied by how the business operates
    
- Future requirements that affect structure

### Rule 1: An Order Must Contain at Least One Book

From IT:

> “A customer cannot place an order without at least one book.”

This directly translates to a **mandatory relationship**.

**Business Rule**

- Every order must be associated with **one or more books**
    

This affects:

- Modality between **Order** and **Book**
    
- Prevents empty or meaningless orders
    

---

### Rule 2: A Book Must Be Uniquely Identified by ISBN

From Store Owner:

> “Each book has an ISBN.”

Even though “unique” is not explicitly stated, ISBNs are **globally unique by definition**.

**Business Rule**

- ISBN uniquely identifies a book
    

This later becomes:

- A **primary key** or **unique constraint**
    

---

### Rule 3: A Customer Can Place Multiple Orders

From Store Owner:

> “Customers can place multiple orders.”

This tells me two things:

- One customer → many orders
    
- An order cannot exist without a customer
    

**Business Rules**

- A customer may place **zero or many orders**
    
- Each order must belong to **exactly one customer**
    

This defines both:

- Cardinality
    
- Modality
    

---

### Rule 4: A Book Can Appear in Multiple Orders

From Operations Team:

> “Each order can contain multiple books.”

This implies the reverse as well.

**Business Rule**

- A book can be included in **multiple orders over time**
    

This confirms a **many-to-many** relationship between Order and Book.

---

### Rule 5: A Book Can Have Multiple Authors

From Store Owner:

> “A book can have multiple authors.”

This tells me:

- One book → many authors
    
- One author → many books
    

**Business Rule**

- Books and authors share a many-to-many relationship
    

---

### Rule 6: Orders Must Be Trackable Over Time

From Operations Team:

> “We want to track order dates.”

This implies:

- Orders are time-bound events
    
- Order history must be preserved
    

**Business Rule**

- Every order must have an associated order date
    

---

### Rule 7: Customers Must Be Contactable

From Operations Team:

> “We need to store customer name, email, and address.”

This tells me these attributes are **mandatory**, not optional.

**Business Rule**

- A customer must have a name, email, and address
    

---

### Rule 8: The Model Must Support Future Expansion

From IT:

> “The system should support future features like reviews and ratings.”

This is a **structural business rule**, not a functional one.

**Business Rule**

- The data model should be extensible
    
- Books should be modeled as independent entities (not embedded inside orders)
    

This influences:

- Normalization
    
- Entity independence
    
