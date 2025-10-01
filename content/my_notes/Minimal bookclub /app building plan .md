---
title: app building plan
draft: false
tags:
  - in-progress
---
## Project Overview

This project is designed as a **learning playground** for:

- **ETL (Extract, Transform, Load)** workflows.
    
- **Relational database design** with PostgreSQL (via Supabase).
    
- Building a **minimal, production-capable app** for small reading clubs.
    
- Adding a **basic ML-powered book recommender** (intro to ML concepts).
    

👉 If you’re new to backend apps, ETL pipelines, or databases, this document walks you step by step.


So , while I was brainstorming and trying to bullet points the idea to have a clear picture on what I want to create , I used the mind map to visualize them. Not everything in the mind map is definite, but I love the idea of using one to ensure it gives me a clear idea on creating one. 

`BOOK CLUB APP`
`├── Database (Postgres/Supabase)`
`│   ├── Users`
`│   ├── Books`
`│   ├── User_Books (ratings, notes, status)`
`│   ├── Groups`
`│   ├── Group_Members`
`│   └── Activity_Logs`
`│`
`├── ETL (External Data → DB)`
`│   ├── Extract → OpenLibrary API / Google Books`
`│   ├── Transform → clean/normalize (title, author, genre)`
`│   └── Load → insert into DB (async SQLAlchemy)`
`│`
`├── CRUD (FastAPI)`
`│   ├── Users: create/list/update/delete`
`│   ├── Books: add/list/update/delete`
`│   ├── Groups: create/join`
`│   └── Logs: track activities`
`│`
`├── Features`
`│   ├── Feeds ("friends finished X", "trending books")`
`│   ├── Recommendations (basic ML)`
`│   └── Search (Postgres FTS, optional pgvector)`
`│`
`├── Performance`
`│   ├── Indexes (B-Tree, GIN)`
`│   ├── Query optimization`
`│   └── Background ETL jobs`
`│`
`└── Frontend (Optional)`
    `├── Next.js/React UI`
    `├── Supabase Auth / JWT`
    `└── Display books, groups, feeds`



The main goal behind working on this project:
## Learning Roadmap

1. **DB Basics** → ER design, Postgres schema, queries.
    
2. **FastAPI + SQLAlchemy** → CRUD routes.
    
3. **ETL** → fetch external data, clean & load into DB.
    
4. **Testing** → pytest + API tests.
    
5. **Features** → groups, activity feeds, logs.
    
6. **ML Intro** → recommender system.
    
7. **Performance** → indexes, monitoring.
    
8. **Frontend (Optional)** → React/Next.js UI.