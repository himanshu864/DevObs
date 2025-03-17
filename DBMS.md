---
tags:
  - backend
references:
  - https://youtu.be/HXV3zeQKqGY?si=CbO_L1udwspvQ_TR
date_created: 2024-06-06
date_modified: 2025-03-17
---
---

Software for creating, managing, and interacting with databases.

- Perform **CRUD** operations (Create Read Update Delete).
- Ensures data consistency, integrity, and security.

**Key Components:**
- Hardware, software, data, procedures, and users.

**DBMS Models:**
- **Relational:** Data stored in tables; uses *[[SQL]]* (Structured Query Language).
- **Non-relational**: using other data structures. JSON, XML, Graphs. *NoSQL*.
	- **Hierarchical:** Tree-like structure.
	- **Network:** Flexible many-to-many relationships.
	- **Object-Oriented:** Stores objects with attributes and methods.

**Advantages:**
- Data abstraction and independence.
- Reduced redundancy.
- Improved data integrity.
- Enhanced security.
- Backup and recovery mechanisms.

**ACID Properties:** Atomicity, Consistency, Isolation, Durability.
- **Atomicity:** Ensures all operations in a transaction complete successfully or none do.
- **Consistency:** Guarantees transactions transition the database between valid states.
- **Isolation:** Keeps concurrent transactions independent to avoid interference.
- **Durability:** Once committed, transaction changes persist even after failures.

**Normalization:** 1NF, 2NF, 3NF to reduce redundancy.
- **First Normal Form (1NF):**
	- Each column contains atomic values.
	- No repeating groups or arrays.
- **Second Normal Form (2NF):**
	- Meets all criteria of 1NF.
	- Eliminates partial dependency; every non-key attribute is fully dependent on the entire primary key.
- **Third Normal Form (3NF):**
	- Meets all criteria of 2NF.
	- Removes transitive dependency; non-key attributes depend only on the primary key.
- **Boyce-Codd Normal Form (BCNF):**
	- A stricter version of 3NF.
	- Every determinant must be a candidate key.

**Core Concepts:**
- **Transactions:** Ensure reliable and consistent operations.
- **Concurrency Control:** Manages simultaneous transactions.
- **Indexing:** Improves data retrieval speed.

**Architectures:**
- **Single-Tier:** Direct access on a single system.
- **Two-Tier:** Client-server model.
- **Three-Tier:** Separates user interface, business logic, and data storage.

**Keys:**
- **Primary Key:** Unique identifier for table records.
- **Foreign Key:** Links records between tables, ensuring referential integrity.
- **Candidate Key:** Minimal attribute set that can uniquely identify records.
- **Composite Key:** Combination of two or more attributes forming a unique identifier.
- **Alternate Key:** Candidate key not chosen as the primary key.

**Data Types:**
- **Numeric:** `INT, FLOAT, DOUBLE, DECIMAL`.
- **Character/String:** `CHAR, VARCHAR, TEXT`.
- **Date/Time:** `DATE, TIME, TIMESTAMP`.
- **Binary:** `BLOB, VARBINARY`.
- **Boolean:** `BIT, BOOL`.

---
