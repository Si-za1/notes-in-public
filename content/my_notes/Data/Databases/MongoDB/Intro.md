---
title: Intro
draft: false
tags:
  - data
---
 
The relational model organizes data into rows and columns within a series of interlinked tables. This model requires an explicit, predefined schema where rules and constraints are applied to the entire database. This means that any future schema changes can require an extensive migration process.

The schema for these tables would be dictated by the third normal form imposed by traditional relational databases, which means that each entity will be stored in only one place in your database. While data modeling in MongoDB follows the same basic concepts, its driving design is different. The main principle is to identify your workload and query patterns, then design your data model to support it.



 In MongoDB, database entities are stored in documents. Documents in MongoDB are presented in a JSON like format, which makes it easy to work with structured, semi structured, and unstructured data across many systems and platforms.
 A key thing to remember with MongoDB is that data accessed together should be stored together.

In MongoDB, **fields are the key value pairs within a document**, similar to columns in a relational database. As you can see, **documents look like JSON objects** you would work with in your applications. Now, instead of storing all of these rows in a table, **documents are stored in collections.** Collections are used to organize related documents. The document model is inherently flexible. The document acts as the schema. This allows us to create similar but different schemas for the same set of entities depending on the needs of our application. 

This flexibility comes **from three core design principles.** 

a. **Polymorphism,** ease of use when working with arrays, and the ability to embed related documents into a parent document. Polymorphism refers to the database's ability to store documents with different structures or fields within the same collection. 
For example, a single books collection can store both print books and ebooks. If you were to represent the same data in a relational database, you would need multiple columns with null values. 

For example, columns like format, file size, and supported devices, which only apply to ebooks, would contain null values for all print book records. This approach creates issues in terms of storage and makes it difficult to adapt to changing requirements. 

b. **Arrays in MongoDB are a powerful tool for flexibility** as well. The value of a field in a document can be an array of values which can themselves be documents.

c. **Embedding** allows you to store documents within parent documents to represent relationships and complex hierarchies. 
For example, Let's say we want to access the top two reviews for our book document when queried. We can simply embed them as sub documents. Now if we wanted to query all books with reviews by the user Jess, we would run this single database operation to retrieve the titles.

The document model also makes it possible to normalize data by referencing other documents from a main document. This is similar to the normalized data model you're familiar with in SQL. You can even mimic a join operation by using the dollar lookup stage.

In MongoDB, you're not constrained to one way of storing data and creating relationships. You can choose to normalize some data, embed other data that will be accessed together, or use any combination of storage methods that make sense for your application.

MongoDB offers schema validation that's enforced by the database itself. You can define rules and constraints, much like in a relational database, to keep your data clean and consistent. The validation occurs directly in the database, no matter which application or user is accessing it. Schema validation also works with polymorphic collections and embedded documents.