---
tags:
  - backend
  - core
references:
  - https://youtu.be/HXV3zeQKqGY?si=CbO_L1udwspvQ_TR
  - https://youtu.be/dl00fOOYLOM?si=DFfMg_7QUuTq7-xv
date_created: 2024-06-06
date_modified: 2025-05-30
---
---
# What is DBMS?
 **Data**: Collection of raw bytes. $\rightarrow$ Process $\rightarrow$ Meaning $\rightarrow$ **Information**.

This information helps understand context and decision making.

**Database**: Electronic place/system where data is stored. Interrelated data.

**DBMS**: Software to perform CRUD operations on database. Generally referred together with DB.

**File Systems Disadvantages over DBMS**
- Data Redundancy and inconsistency.
- Difficulty in accessing data and querying.
- Data isolation.
- Integrity problems.
- Atomicity problems.
- Concurrent-access anomalies.
- Security problems.

**Key Components:**
- Hardware, software, data, procedures, and users.

**DBMS Models:**
- **Relational:** Data stored in tables; uses *[[SQL]]* (Structured Query Language).
- **Non-relational**: using other data structures. JSON, XML, Graphs. *NoSQL*.
	- **Hierarchical:** Tree-like structure.
	- **Network:** Flexible many-to-many relationships.
	- **Object-Oriented:** Stores objects with attributes and methods.

**Advantages:**
- Data abstraction and independence (hiding complex details and giving simple concise output).
- Reduced redundancy (repetition of same data in multiple tables).
- Improved data integrity (information remains accurate, complete and consistent).
- Enhanced security (authorization).
- Backup and recovery mechanisms.

**ACID Properties:** Atomicity, Consistency, Isolation, Durability.
- **Atomicity:**
	- Ensures all operations in a transaction complete successfully or none do.
	- Eg: During a 100$ transactions, $A$'s balance should be reduce and $B$'s balance should increment at the same time. During failure, both balances should return to normal.
- **Consistency:**
	- Guarantees transactions transition the database between valid states.
	- Eg: Ones balance shouldn't be negative. Hence a 100$ transaction from an account with balance 50$ failed due to consistency violation.
- **Isolation:**
	- Keeps concurrent transactions independent to avoid interference.
	- *Dirty read* - when a transaction reads data that has been modified by another transaction but that transaction has not yet committed its changes.
	- *Non-repeatable read* - when a transaction reads the same row twice, but the second read retrieves different values than the first.
	- *Phantom read* - when a transaction re-executes a query and finds that the results have changed due to the insertion or deletion of rows by another transaction, even though the initial transaction hadn't modified anything itself.
- **Durability:**
	- Once committed, transaction changes persist even after failures.
	- By using *Write-Ahead Logging* and replication, making changes permanent.

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
# DBMS Architecture

### View of Data

- DBMS provide users with an **abstract view** of data. No details about how data is stored, maintained or accessed.
- Three-level architecture enables personalized view of data.

#### 1. Physical level / Internal level

- Lowest level abstraction.
- Low level data structures are used.
- *Physical Schema* describes physical storage structure of DB.
- Data compression, encryption, hashing, etc.
- Algorithms to access data efficiently.

#### 2. Logical level / Conceptual level

- *Conceptual schema* to describe data and it's relationships.
- Doesn't care about physical-level structures. Leading to **Physical data independence**. Change in physical schema doesn't affect logical schema.
- *Database Administration* decides what information to keep in DB uses logical level of abstraction.

#### 3. View level / External level

- Highest level of abstraction to provide personalized data view.
- Several schema called **subschema** for different views.
- Also provides *security* mechanism to prevent users from unauthorized access.

![[Pasted image 20250328131055.png | 500]]

### Instance and Schema

- **Instance**: Collection of information stored in DB at any given instance.
- **Schema**: structural description of data.
- Logical schema is most important subschema.

### Data models

- Provides way to design DB at logical level by defining data relationships, constraints, semantics, etc.
- Eg: ER model, Relational model, Object-oriented model, object-relational model, etc.

### Database Languages

- **Data Definition Language (DLL)**: to define/specify DB schema.
- **Data manipulation language (DML)**: to perform DB queries and updates (CRUD).
- SQL provides features of both languages.

### Database access from Application

- An interface is created for two non-compatible languages to communicate with each other.
- API is used to send queries to DB and fetch results.
	- **Open Database Connectivity (ODBC)**: C/C++.
	- **Java Database Connectivity (JDBC)**: Java.

### Database Architecture (DBA)

- Person who has central control of both data and program that access that data.
- Is responsible for:
	- Schema Definition.
	- Storage structure and access methods.
	- Schema and physical organization modifications.
	- Authorization control.
	- Routine maintenance (periodic backups, security patches, upgrades, etc)

### Database Application Architecture

**Tier-1 Architecture**
- Client, server and database on the same machine.

**Tier-2 Architecture**

- Client communication with DB server. No third party.
- API standards like ODBC and JDBC are used interact.

![[Pasted image 20250328140730.png | 400]]

**Tier-3 Architecture**

![[Pasted image 20250328142004.png | 400]]

- Different client, server, and database.
- For business applications. Scalable, Data Integrity, Security.

---
# ER Model

High level data model based on a perception of a real world that consists of a collection of basic objects, called **entities** and of **relationships** among these objects.

- ER Diagram is graphical representation of ER Model.
- Entity: Thing or object in real world that is distinguishable from other objects.
- **Strong Entity**: can be uniquely identified using primary key.
- **Weak Entity**: can't be uniquely identified, depends on some other strong entity.
- **Entity Set**: set of similar type of entities that share the same attributes. Eg: Students.

**Attribute**
An entities property(s). Has a set permitted values called *domain* or value set.

**Types of Attributes:**

1. **Simple**: can't be divided further. Eg: Phone number.
2. **Composite**: can be divided into further attributes. Eg: Address.
3. **Single-valued**: one value attribute. Eg: Student ID.
4. **Multi-valued**: more than one value. Eg: Phone number.
5. **Derived**: can be derived from other related attributes. Eg: Age from DOB.

Attributes takes null value when no value for it. Eg: Middle name (not applicable). Can also indicate value is unknown (data inconsistency).

![[Screenshot 2025-03-29 at 6.35.14 PM.png]]

**Relationships**: association among two or more entities. Eg: customer *places* order.

- **Strong** relationship: between two independent entities. Eg: Loan
- **Weak** relationship: between weak entity and it's owner/strong entity. Eg: payment.
- **Degree of relationship**: number of entities participating in a relationship.
	1. *Unary*: only one entity participates. Eg: employee manages employee.
	2. *Binary*: two entity participates. Eg: student takes course.
	3. *Ternary*: three entity. Eg: Teacher teaches student, teacher teaches subject.
- **Relationship constraints**
	- Mapping cardinality / cardinality ratio:
		1. *One to one*: Entity A associates with at most one entity B and vice-versa. Eg: Citizen has Aadhar-card.
		2. *One to many*: Entity A associates with N entity B. While entity B associates with at most one entity A. Eg: Citizen has vehicle.
		3. *Many to one*: opposite of one-many. Eg: employee and department.
		4. *Many to many*: Entity A associates with N entity B. and vice-versa. Eg: Students and course.
	- Participation Constraints: Minimum cardinality constraints. Types:
		1. *Partial participation*: not all entities are involved in the relationship instance.
		2. *Total participation*: each entity must be involved in at least one relationship instance.
		3. Weak entity has total participation constraints, but strong may not.
