## Contents
1. [[#Section 1 Fundamentals of DBMS]]
2. [[#Section 2 Database Models & Structures]]
3. [[#Section 3 Database Design and Modeling]]
4. [[#Section 4 Transactions & Concurrency]]
5. [[#Section 5 Data Storage, Indexing & Performance]]

## Section 1: Fundamentals of DBMS
This foundational section deconstructs the Database Management System (DBMS), moving from its high-level purpose and operational environment to its internal software components. It establishes the essential vocabulary and architectural principles that govern all subsequent topics.

### What is a DBMS? Purpose & Core Functions
A Database is an organized collection of various kinds of data. For example, a company database may include their employees' details, sales data. product information, etc.

A Database Management System (DBMS) is a software system designed to create, manage, and interact with databases. It acts as an intermediary between the user or application and the physical database, providing a structured and efficient way to handle large volumes of data. It allows efficient addition, retrieval, modification and deletion of stored data.

The core functions of a DBMS can be categorized into four main areas:
1. **Data Definition**: This involves defining the structure, or schema, of the database. Users can specify the types of data to be stored, create tables, define relationships between them, and establish constraints to maintain data integrity.
2. **Data Manipulation**: This function allows users to insert new data, update existing records, and delete obsolete information. A DBMS provides the tools to perform these operations efficiently and safely.
3. **Data Retrieval**: A key function of a DBMS is to provide users with the ability to query the database to retrieve specific information. This is often accomplished through a specialized query language.
4. **Administration**: This encompasses a wide range of management tasks, including enforcing data security by controlling user access, ensuring data integrity through constraints, managing concurrency to allow multiple users to work simultaneously without conflict, and performing regular backups and recovery procedures to prevent data loss.

#### Database Schema
Data abstraction manages complexity by hiding unnecessary details from the user. A schema is a description of how data will be stored in a database and defines the basic database structure.

Schemas are created at three levels of Abstraction:
1. A **Physical Schema** describes the database design at the physical level in the form of files, etc.
2. A **A Logical Schema** is a conceptual understanding of data representing the database at a logical level.
3. A **View Schema** is the user representation of design and describes the database at an application level. 

### Key Components of a DBMS Environment
A functional DBMS does not operate in isolation; it is part of a larger, integrated environment. Understanding this ecosystem is essential to appreciating the role and dependencies of the database system. The environment is composed of five principal components.
1. **Hardware**: This refers to the physical electronic devices on which the database system runs. It includes servers with sufficient processing power (CPU) and memory (RAM), as well as storage devices like hard disk drives (HDDs) or solid-state drives (SSDs) where the data is physically stored. The performance and capacity of the hardware directly constrain the capabilities of the DBMS.

2. **Software**: This component includes the DBMS application itself (e.g., Oracle, MySQL, PostgreSQL), the underlying operating system (e.g., Linux, Windows Server) that manages the hardware, the network software that enables communication between clients and the server, and the various application programs that use the database to perform business functions.

3. **Data**: As the central asset, data encompasses the collection of raw facts stored in the database. This includes not only the operational data (e.g., customer records, sales transactions) but also the metadata, or "data about the data." Metadata describes the database schema, such as table names, column data types, and constraints, and is essential for the DBMS to manage and interpret the operational data.

4. **Procedures**: These are the formal rules and instructions that govern the design and use of the database. Procedures dictate how users should interact with the system, including protocols for logging in, running backups, and handling system failures. These guidelines ensure that the database is operated in a consistent and secure manner.

5. **Users/People**: This component includes all individuals who interact with the database, each with a distinct role. End-users may interact with the data through application interfaces. Application programmers develop the software that uses the database. The most critical role is that of the Database Administrator (DBA), who is responsible for the overall management, maintenance, security, and performance of the entire DBMS environment.

### The Internal Architecture of a DBMS
The DBMS software itself is a complex system of interconnected modules, each responsible for a specific aspect of data management. The separation of these components is a deliberate and critical design choice that enables flexibility, modularity, and optimization. For instance, the division between the query processor and the storage engine allows a single database system to support different underlying storage mechanisms (e.g., one for transactional workloads, another for analytical ones) without altering the way users write queries. This architectural modularity is a foundational principle of modern DBMS design and explains the versatility of systems like MySQL, which supports pluggable storage engines such as InnoDB and MyISAM.

The primary internal components include:
- **Storage Engine**: This is the core component that handles the physical interaction with the data. It is responsible for writing data to and reading data from the disk, managing memory, and handling the low-level data structures. All requests to access or modify data must pass through the storage engine.

- **Query Processor**: Often considered the "brain" of the DBMS, the query processor is responsible for interpreting, optimizing, and executing user queries. It receives a declarative query (a statement of _what_ data is needed) and devises an imperative execution plan (a procedure for _how_ to get it). It consists of several sub-components, including a parser to check syntax, an optimizer to find the most efficient execution path, and an execution engine to carry out the plan.

- **Metadata Catalog (Data Dictionary)**: This is a system-level database that stores metadata. It contains information about the database schema, including definitions of tables, columns, data types, indexes, constraints, and user permissions. The query processor relies heavily on the metadata catalog to validate queries and formulate execution plans.

- **Log Manager**: This component maintains a detailed record, or log, of all modifications made to the database. This transaction log is indispensable for ensuring the durability of committed transactions and for recovering the database to a consistent state in the event of a system failure.

### Database Languages Overview
Interaction with a DBMS is facilitated through specialized languages, which can be categorized based on their function. While SQL (Structured Query Language) is the most common implementation, the conceptual categories are universal across most database systems.
1. **Data Definition Language (DDL)**: DDL commands are used to define and manage the database's structure or schema. This includes operations for creating, altering, and deleting database objects like tables, indexes, and views.
2. **Data Manipulation Language (DML)**: DML commands are used to manage the data within the schema objects. This category includes operations for inserting new records, updating existing ones, and deleting data from tables.
3. **Data Control Language (DCL)**: DCL commands are concerned with the security and access control aspects of the database. They are used to grant permissions to users and to revoke them, ensuring that only authorized individuals can access or modify the data.
4. **Transaction Control Language (TCL)**: TCL commands are used to manage transactions within the database. These commands ensure that transactions are executed as atomic units of work, allowing users to make a set of changes permanent (commit) or undo them (rollback).

> [!seealso] 
> For in-depth explanations on SQL and its clauses please refer [[SQL Cheatsheet]]


## Section 2: Database Models & Structures
This section explores the logical frameworks used to organize data. It begins with a deep dive into the dominant relational model and then provides a comparative analysis against both its historical predecessors and modern NoSQL alternatives, highlighting the evolutionary pressures that led to their development.

### The Relational Model
The relational model, conceived by Edgar F. Codd in 1969, provides the theoretical foundation for the vast majority of modern database systems. It is an abstract model that organizes data into two-dimensional tables, known as relations. The model's enduring power stems from its mathematical rigor, rooted in set theory and first-order predicate logic, which enables users to specify data and queries declaratively.

The core terminology of the relational model is precise:
- **Relation**: A table consisting of columns and rows.
- **Tuple**: A single row within a relation, representing a specific instance of an entity (e.g., one particular student).
- **Attribute**: A single column within a relation, representing a property of the entity (e.g., `StudentName`).
- **Domain**: The set of all legal, atomic values that an attribute can hold (e.g., the domain for a `Grade` attribute might be the set of integers from 0 to 100).
- **Degree**: The total number of attributes (columns) in a relation.
- **Cardinality**: The total number of tuples (rows) in a relation.

#### Codd's Rules for Relational Databases
Dr. Edgar F. Codd, the creator of the relational model, proposed a set of thirteen rules (0 to 12) to define the criteria for a database management system to be considered a true Relational DBMS (RDBMS). These rules were intended to prevent the dilution of his relational vision as vendors began to repackage older products with a "relational" label.

| Rule Name                                 | Description                                                                                                                                                                                                                    |
| ----------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Foundation Rule**                       | The system must manage the database entirely through its relational capabilities. This is the fundamental principle upon which all other rules are based.                                                                      |
| **Information Rule**                      | All information in the database, including user data and metadata, must be represented explicitly and solely as values within tables (rows & columns).                                                                         |
| **Guaranteed Access Rule**                | Every single atomic value in the database must be logically accessible by a combination of its table name, primary key value, and column name.                                                                                 |
| **Systematic Treatment of NULL Values**   | NULL values must be supported and handled systematically to represent missing or inapplicable information, distinct from zero, empty strings, or other values.                                                                 |
| **Active Online Catalog**                 | The database description (metadata) must be stored online in the same relational format as ordinary data, allowing authorized users to query it with the same relational language.                                             |
| **Comprehensive Data Sub-language**       | The system must support at least one comprehensive language with a well-defined syntax that can handle data definition, data manipulation, integrity constraints, and transaction management.                                  |
| **View Updating Rule**                    | All views that are theoretically updatable must also be updatable by the system.                                                                                                                                               |
| **High-Level Insert, Update, and Delete** | The system must support set-at-a-time operations for insertion, updating, and deletion, not just single-row operations. This includes support for set operations like UNION, INTERSECTION, and MINUS.                          |
| **Physical Data Independence**            | Application programs and user activities must remain logically unimpaired when changes are made to physical storage representations or access methods.                                                                         |
| **Logical Data Independence**             | Application programs and user activities must remain logically unimpaired when information-preserving changes are made to the base tables (e.g., splitting a table).                                                           |
| **Integrity Independence**                | Integrity constraints must be definable in the relational data language and stored in the catalog, not within individual application programs.                                                                                 |
| **Distribution Independence**             | The distribution of data across various physical locations should be invisible to the end-user. The user should always perceive the data as being located at a single site.                                                    |
| **Non-Subversion Rule**                   | If the system provides a low-level (single-record-at-a-time) interface, that interface must not be able to be used to subvert or bypass the integrity rules and constraints expressed in the higher-level relational language. |

### Alternative Data Models: Hierarchical & Network Models
Before the relational model became dominant, earlier models were used to structure data, each with distinct characteristics and limitations.
1. **Hierarchical Model**: Earliest Model developed in the 1950s by IBM. This model organizes data in a tree-like structure. Each record has a single parent, and each parent can have one or more child records. This creates a strict one-to-many relationship. While simple to understand, its rigidity is a significant drawback, as it cannot naturally represent many-to-many relationships.
2. **Network Model**: An evolution of the hierarchical model, the network model allows a record (called a "member") to have multiple parent records (called "owners"). This is achieved by representing data as a graph, enabling the modeling of more complex, many-to-many relationships. However, this flexibility came at the cost of increased complexity in navigating and managing the database.


## Section 3: Database Design and Modeling
This section transitions from abstract models to the practical discipline of designing a robust, efficient, and maintainable database. The entire process can be viewed as a structured translation from human-centric business requirements into a logically sound and physically efficient machine-readable format. It begins with the conceptual **ER Model** to capture business needs, formalizes these needs into logical rules using **Functional Dependencies**, applies the algorithmic process of **Normalization** to refine the structure and eliminate anomalies, and finally, implements these rules through **Keys** that enforce integrity within the database schema.

### The Entity-Relationship (ER) Model
The Entity-Relationship (ER) model is a high-level, conceptual data modeling technique used to visualize the structure of a database before its physical implementation. It provides a graphical representation that is easy for both technical and non-technical stakeholders to understand.

The core components of an ER diagram are :
1. **Entity:** An entity represents a real-world object, concept, or event about which data is collected. Examples include `Student`, `Course`, or `Professor`. In an ER diagram, an entity type is typically represented by a **Rectangle**. Types of Entities are:
	1. **Strong Entity:** It has a key Attribute and does not depend on any other entity in the Schema. Has a PK which identifies it uniquely.
	2. **Weak Entity:** Key attribute can't be defined, or it depends on another entity in the schema. Represented by a **Double Rectangle**.

2. **Attribute:** An attribute is a property or characteristic of an entity. For example, the `Student` entity might have attributes like `StudentID`, `StudentName`, and `DateOfBirth`. Attributes are often depicted as **Ellipses** connected to their entity. Types of Attributes are:
	1. **Key Attribute:** Which Uniquely identifies each entity in an Entity Set.
	2. **Composite Attribute:** Composed of many other attributes.
	3. **Multivalued Attribute:** Consisting of more than 1 value for an Entity.
	4. **Derived Attribute:** Can be derived from other attributes of the Entity.

3. **Relationship:** A relationship represents an association between two or more entities. For instance, a `Student` _enrolls in_ a `Course`. Relationships are typically shown as **Diamond** shapes connecting related entities with **Lines**.

4. **Cardinality:** Number of times an entity can participate in a relationship is called cardinality. It specifies the number of instances of one entity that can be associated with instances of another entity. The common cardinalities are:
	1. **One-to-One (1:1)**: Each entity instance is related to exactly one instance of the other entity.
	2. **One-to-Many (1:N/N:1)**: One entity instance can be related to multiple instances of another entity, but each of those instances is related to only one instance of the first.
	3. **Many-to-Many (M:N)**: Instances of each entity can be related to multiple instances of the other entity

### The Extended ER (EER) Model
As data complexity grows, the standard ER model can become insufficient for representing intricate real-world scenarios. The Extended Entity-Relationship (EER) model builds upon the basic ER model by introducing advanced concepts to handle more complex applications and data relationships.  

The primary features of the EER model are:
#### Specialization and Generalization
These two concepts represent opposite sides of the same coin, establishing a hierarchical relationship between a higher-level entity set (superclass) and one or more lower-level entity sets (subclasses). This is also known as an "IS-A" relationship (e.g., a Manager "IS-A" Employee).
1. **Specialization**: This is a **top-down** process where a general entity (superclass) is divided into more specific subgroups (subclasses) based on distinguishing characteristics. For example, the `Employee` entity could be specialized into subclasses like `Secretary`, `Engineer`, and `Technician`, each with its own specific attributes (e.g., `Typing_speed` for a Secretary).

2. **Generalization**: This is a **bottom-up** process where multiple specific entities that share common attributes are combined to form a more general superclass. For instance, the entities `Car`, `Bus`, and `Motorcycle` can be generalized into a single `Vehicle` superclass that holds common attributes like `Vehicle_id` and `License_plate_no`. This process abstracts common features and reduces redundancy.

3. **Inheritance**: A key feature of this hierarchy is inheritance. Subclasses inherit all the attributes and relationships of their superclass, promoting reusability and data consistency.  

**Constraints on Specialization:** Specialization can be further defined by two types of constraints :  
1. **Disjoint vs. Overlapping**:
    - **Disjoint**: An entity can belong to only one subclass. For example, an `Employee` cannot be both a `Salaried_Employee` and an `Hourly_Employee` simultaneously.
    - **Overlapping**: An entity can belong to multiple subclasses. For example, a university `Employee` might also be a `Student`.  
2. **Total vs. Partial Participation**:
    - **Total**: Every entity in the superclass must belong to at least one subclass. This is indicated by a double line in ER diagrams. For example, every `Employee` must be either `Salaried` or `Hourly`.
    - **Partial**: An entity in the superclass is not required to belong to any subclass. For example, not every `Employee` is necessarily a `Manager`.  

#### Aggregation
Aggregation is a process used to model a "relationship among relationships." It treats a relationship set as a higher-level, abstract entity, allowing it to participate in other relationships. This is necessary when the basic ER model cannot directly represent relationships between other relationships. Aggregation is used to eliminate redundancy and represent complex scenarios more clearly. 

**Example**: 
Consider a scenario where an `Employee` `works_on` a `Project` at a specific `Branch`. This `works_on` relationship itself needs to be managed by a `Manager`. Instead of creating multiple, potentially redundant relationships between `Manager` and the other entities, aggregation allows us to treat the `works_on` relationship as a single abstract entity. We can then create a `manages` relationship between the `Manager` entity and this new aggregated entity.

### Functional Dependencies
A functional dependency (FD) is a formal constraint between two sets of attributes in a relation. It is the logical foundation upon which database normalization is built. An FD is denoted as X→Y, which is read as "X functionally determines Y." This means that for any given value of attribute set X, there is exactly one corresponding value for attribute set Y.

For example, in a `Students` table, the functional dependency `StudentID \rightarrow StudentName` holds because each unique `StudentID` corresponds to exactly one `StudentName`.

The main types of functional dependencies are:
1. **Trivial Functional Dependency**: Occurs if the dependent attributes (Y) are a subset of the determinant attributes (X). For example, {StudentID,StudentName}→StudentName. These are always true and are not useful for normalization.
2. **Non-Trivial Functional Dependency**: Occurs if at least one attribute in Y is not part of X. For example, `StudentID \rightarrow StudentName`. These are the dependencies that are critical for normalization.
3. **Transitive Dependency**: An indirect dependency where A→B and B→C, but B does not determine A. This implies an indirect dependency A→C. For example, if `StudentID \rightarrow DepartmentID` and `DepartmentID \rightarrow DepartmentHead`, then there is a transitive dependency `StudentID \rightarrow DepartmentHead`. Eliminating such dependencies is the goal of the Third Normal Form (3NF).

### Database Normalization & Forms
Normalization is a systematic process of organizing the columns and tables in a relational database to minimize data redundancy and improve data integrity. The primary goal is to eliminate undesirable characteristics known as **insertion, update, and deletion anomalies**, which can arise in poorly designed tables.

The process is hierarchical, with each normal form building upon the previous one. A step-by-step example illustrates the process:

**Unnormalized Table:**
Consider a table of project assignments:

|ProjectID|ProjectName|EmployeeID|EmployeeName|EmployeeSkills|
|---|---|---|---|---|
|P101|Apollo|E01|John Smith|Java, Python|
|P102|Gemini|E02|Jane Doe|SQL|
|P101|Apollo|E02|Jane Doe|SQL|

This table suffers from multiple issues, including multi-valued attributes (`EmployeeSkills`) and significant redundancy (`ProjectName` and `EmployeeName` are repeated).

**Step 1: Achieve First Normal Form (1NF)**
A table is in 1NF if all its attribute values are atomic (indivisible). The `EmployeeSkills` column violates this rule. To conform to 1NF, we eliminate the repeating group by creating a separate row for each skill.
**1NF Table:**

| ProjectID                                             | ProjectName | EmployeeID | EmployeeName | EmployeeSkill |
| ----------------------------------------------------- | ----------- | ---------- | ------------ | ------------- |
| P101                                                  | Apollo      | E01        | John Smith   | Java          |
| P101                                                  | Apollo      | E01        | John Smith   | Python        |
| P102                                                  | Gemini      | E02        | Jane Doe     | SQL           |
| P101                                                  | Apollo      | E02        | Jane Doe     | SQL           |
| _Primary Key: {ProjectID, EmployeeID, EmployeeSkill}_ |             |            |              |               |

**Step 2: Achieve Second Normal Form (2NF)**
A table is in 2NF if it is in 1NF and all non-key attributes are fully functionally dependent on the entire primary key. In our 1NF table, we have partial dependencies:
1. `ProjectID -> ProjectName` (`ProjectName` depends only on a part of the primary key).
2. `EmployeeID -> EmployeeName` (`EmployeeName` depends only on a part of the primary key).
To resolve this, we decompose the table into smaller tables:

**Projects Table (2NF):**

|ProjectID|ProjectName|
|---|---|
|P101|Apollo|
|P102|Gemini|
|_Primary Key: {ProjectID}_||

**Employees Table (2NF):**

|EmployeeID|EmployeeName|
|---|---|
|E01|John Smith|
|E02|Jane Doe|
|_Primary Key: {EmployeeID}_||

**EmployeeSkills Table (2NF):**

|EmployeeID|EmployeeSkill|
|---|---|
|E01|Java|
|E01|Python|
|E02|SQL|
|_Primary Key: {EmployeeID, EmployeeSkill}_||

**ProjectAssignments Table (2NF):**

|ProjectID|EmployeeID|
|---|---|
|P101|E01|
|P102|E02|
|P101|E02|
|_Primary Key: {ProjectID, EmployeeID}_||

**Step 3: Achieve Third Normal Form (3NF)**
A table is in 3NF if it is in 2NF and there are no transitive dependencies. Let's modify the Employees table to include department information:

**Employees Table (violates 3NF):**

| EmployeeID | EmployeeName | DeptID | DeptName    |
| ---------- | ------------ | ------ | ----------- |
| E01        | John Smith   | D01    | Engineering |
| E02        | Jane Doe     | D02    | Marketing   |

Here, `EmployeeID -> DeptID` and `DeptID -> DeptName`. This creates a transitive dependency: `EmployeeID -> DeptName`. To achieve 3NF, we decompose again:

**Employees Table (3NF):**

|EmployeeID|EmployeeName|DeptID|
|---|---|---|
|E01|John Smith|D01|
|E02|Jane Doe|D02|
|_Primary Key: {EmployeeID}_|||

**Departments Table (3NF):**

|DeptID|DeptName|
|---|---|
|D01|Engineering|
|D02|Marketing|
|_Primary Key: {DeptID}_||

**Step 4: Achieve Boyce-Codd Normal Form (BCNF)**
BCNF is a stricter version of 3NF. A table is in BCNF if, for every non-trivial functional dependency X→Y, X is a superkey. BCNF addresses certain rare anomalies not handled by 3NF.

### Database Keys: The Pillars of Integrity
Keys are attributes or sets of attributes that serve to uniquely identify records and establish relationships, thereby enforcing the logical structure defined during normalization.

| Key Type          | Definition                                                                                                    | Purpose                                                                       | Example (in a `Students` table)                                                                                        |
| ----------------- | ------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| **Superkey**      | A set of one or more attributes that, taken collectively, uniquely identifies a tuple in a relation.          | To provide a basis for identifying unique rows.                               | `{StudentID}`, `{StudentSSN}`, `{StudentID, StudentName}` are all superkeys.                                           |
| **Candidate Key** | A minimal superkey; a superkey from which no attribute can be removed without losing the uniqueness property. | To identify all possible unique identifiers for a relation.                   | `{StudentID}` and `{StudentSSN}` are candidate keys. `{StudentID, StudentName}` is not, as `StudentName` is redundant. |
| **Primary Key**   | The candidate key selected by the database designer to be the principal means of identifying tuples.          | To serve as the main, non-null, unique identifier for every row in the table. | The designer chooses `{StudentID}` as the primary key.                                                                 |
| **Alternate Key** | A candidate key that was not selected to be the primary key.                                                  | To provide alternative unique identifiers for rows.                           | `{StudentSSN}` becomes the alternate key.                                                                              |
| **Foreign Key**   | An attribute in one table that refers to the primary key of another table.                                    | To create a link between tables and enforce referential integrity.            | A `CourseEnrollments` table might have a `StudentID` column that is a foreign key referencing the `Students` table.    |
| **Composite Key** | A primary key that consists of two or more attributes.                                                        | To uniquely identify a record when a single attribute is not sufficient.      | In the `CourseEnrollments` table, the primary key might be `{StudentID, CourseID}`.                                    |


## Section 4: Transactions & Concurrency
This section addresses the dynamic aspects of a DBMS, focusing on how it handles data modifications and simultaneous user access while guaranteeing reliability and consistency. The mechanisms discussed here are crucial for maintaining the integrity of data in multi-user environments.

### Transactions & their States
A transaction is a single, logical unit of work that consists of one or more database operations, such as reading, inserting, updating, or deleting data. From the perspective of the DBMS, a transaction is an indivisible operation; it must either complete in its entirety or not at all.

A transaction progresses through a series of states during its lifecycle:
1. **Active**: The initial state where the transaction is executing its operations.
2. **Partially Committed**: This state is reached after the last operation of the transaction has been executed. The changes are not yet permanent and are stored in temporary buffers.
3. **Committed**: If the transaction completes successfully, it enters the committed state. All changes made during the transaction are permanently saved to the database.
4. **Failed**: If the transaction encounters an error or cannot proceed, it enters a failed state.
5. **Aborted**: Following a failure, the transaction is aborted. The DBMS must then roll back any changes made, restoring the database to its state before the transaction began.
6. **Terminated**: This is the final state of the transaction, reached after it has either been committed or aborted.

![[transaction-states.excalidraw.png]]

### The ACID Properties
The reliability of transactions in a DBMS is guaranteed by a set of four properties known collectively as ACID. These properties form a contract that ensures data integrity even in the event of errors, power failures, or other mishaps.32 The classic example of a bank transfer of $100 from Account A to Account B effectively illustrates these properties.
1. **Atomicity**: This property ensures that a transaction is an "all or nothing" proposition. In the bank transfer, two operations must occur: debiting $100 from Account A and crediting $100 to Account B. Atomicity guarantees that if either of these operations fails, the entire transaction is rolled back, and the account balances remain unchanged. The database is never left in a partially updated state.

2. **Consistency**: This property ensures that a transaction brings the database from one valid state to another. A valid state is one that satisfies all defined rules and constraints. In the bank transfer example, a consistency rule might be that the total sum of money in both accounts must remain constant. The transaction is valid only if it preserves this rule. If the transaction were to create or destroy money, it would violate consistency and be rolled back.

3. **Isolation**: This property ensures that concurrent transactions do not interfere with one another. If multiple transactions are executing simultaneously, the system must behave as if they were executed serially (one after another). For instance, if another process is calculating the total assets of the bank while the transfer is in progress, isolation guarantees that it will see the state of the accounts either entirely before the transfer or entirely after it, but never an intermediate, inconsistent state where the money has left Account A but not yet arrived in Account B.

4. **Durability**: This property guarantees that once a transaction has been successfully committed, its changes are permanent and will survive any subsequent system failure, such as a power outage or server crash. In the bank transfer, once the user receives confirmation, the updated balances are permanently recorded and will not be lost.

### Concurrency Control
In most database systems, multiple users need to access and modify data simultaneously. This concurrent execution is essential for system performance and throughput. 

However, uncontrolled concurrency can lead to several problems that compromise data integrity:
1. **Lost Update Problem**: Occurs when two transactions access the same data item, and one transaction's update is overwritten by the other's.
2. **Dirty Read Problem**: Occurs when a transaction reads data that has been modified by another transaction that has not yet committed. If the modifying transaction is later rolled back, the first transaction will have read invalid, "dirty" data.
3. **Inconsistent Retrieval Problem**: Occurs when a transaction accesses several data items, but another transaction modifies some of them during the execution of the first transaction, leading to an inconsistent view of the data.

The goal of concurrency control is to manage the interleaved execution of transactions to prevent these issues. This is achieved by ensuring **serializability**, which means that the outcome of the concurrent execution is equivalent to some serial execution of the same transactions.

### Concurrency Control Mechanisms
The theoretical guarantee of "Isolation" from the ACID properties is implemented in practice as a spectrum of trade-offs. A system can offer very strict isolation, which guarantees correctness but may limit performance, or it can offer weaker isolation levels that allow for greater concurrency at the risk of certain anomalies. The choice of a concurrency control mechanism is the engineering solution to this fundamental trade-off between data correctness and system performance.

The primary mechanisms used to enforce concurrency control are:
1. **Lock-Based Protocols**: This is a pessimistic approach where transactions must acquire a lock on a data item before accessing it. Locks prevent other transactions from performing conflicting operations.
    - **Shared Lock (S-lock)**: Also known as a read lock. If a transaction holds an S-lock on an item, other transactions can also acquire an S-lock to read the item, but no transaction can acquire an exclusive lock to write to it.
    - **Exclusive Lock (X-lock)**: Also known as a write lock. If a transaction holds an X-lock on an item, no other transaction can acquire any lock (shared or exclusive) on that item.
    - **Two-Phase Locking (2PL)**: A common protocol that ensures serializability by dividing a transaction's life into two phases: a "growing phase," where it can acquire locks but not release any, and a "shrinking phase," where it can release locks but not acquire new ones.
        
2. **Timestamp-Based Protocols**: In this approach, every transaction is assigned a unique timestamp when it starts. The DBMS then ensures that any conflicting read and write operations are executed in timestamp order. If an operation violates this order, the transaction is aborted and restarted with a new timestamp. This method is deadlock-free.

3. **Multi-Version Concurrency Control (MVCC)**: This is an optimistic approach that allows reads and writes to proceed concurrently without blocking each other. Instead of using locks, the database maintains multiple versions of a data item. When a transaction needs to read an item, the DBMS provides it with a snapshot of the data as it existed at the start of the transaction. Writes create a new version of the data item. This allows readers to access old data without being blocked by writers, significantly improving concurrency, especially in read-heavy workloads.


## Section 5: Data Storage, Indexing & Performance
This section bridges the gap between the logical database design and its physical implementation. The performance of a database is not determined by a single factor but is an emergent property arising from the interplay between the logical model, the physical storage architecture, and the intelligence of the query processor. A slow query is rarely just a "bad query"; it is often a symptom of a mismatch between the query's needs and the underlying structure.

### Physical Data Storage
While data is conceptually viewed in two-dimensional tables, it must be serialized into a one-dimensional stream of bytes for storage on disk or in memory. The method of serialization has profound implications for performance.
1. **Row-Oriented Storage**: In this traditional model, all the data for a single row (tuple) is stored contiguously on disk. This approach is optimized for Online Transaction Processing (OLTP) workloads, where applications frequently need to read or write entire records at once, such as retrieving a specific customer's complete profile or inserting a new order.

2. **Column-Oriented (Columnar) Storage**: In this model, all values for a single column (attribute) are stored contiguously. This approach is highly optimized for Online Analytical Processing (OLAP) workloads, which are common in data warehousing and analytics. When a query needs to aggregate data from only a few columns across millions of rows (e.g., calculating the average sales amount for all transactions), a columnar database only needs to read the data for those specific columns, drastically reducing I/O compared to a row-oriented system. This format also allows for significantly better data compression, as all data in a column is of the same type and often has similar values.

|Characteristic|Row-Oriented|Column-Oriented|
|---|---|---|
|**Data Storage Pattern**|Data for an entire row is stored together.|Data for an entire column is stored together.|
|**Best for Workload**|Transactional (OLTP)|Analytical (OLAP)|
|**Read Performance**|Fast for retrieving entire rows.|Fast for reading a subset of columns across many rows.|
|**Write Performance**|Fast for inserting or updating single rows.|Generally slower for single-row updates; prefers batch operations.|
|**Compression Efficiency**|Lower|Higher, due to data homogeneity within columns.|
|**Common Use Cases**|E-commerce sites, banking systems, operational applications.|Data warehouses, business intelligence, big data analytics.|


### Database Indexing
An index is a specialized data structure that provides a fast lookup path to data in a table, much like the index in the back of a book. It improves the speed of data retrieval operations but comes at the cost of increased storage space and slower write operations (inserts, updates, and deletes), as the index must also be updated.
1. **The B-Tree Structure**: The B-Tree is the most prevalent data structure used for implementing indexes in relational databases. It is a self-balancing tree structure that keeps its keys in sorted order, allowing for efficient searches, insertions, and deletions in logarithmic time. A B-Tree consists of a root node, intermediate branch nodes, and terminal leaf nodes. By traversing the tree from the root down, the database can quickly locate the desired data without having to scan the entire table.

2. **Clustered vs. Non-Clustered Indexes**: The distinction between these two index types is a frequent point of confusion but is critical to understanding database performance.
    - A **Clustered Index** determines the physical order of the data rows in a table. The leaf nodes of the B-Tree in a clustered index contain the actual data pages. Because the data can only be physically sorted in one way, a table can have only one clustered index. An analogy is a dictionary, where the words (the data) are physically sorted in alphabetical order (the index).
    - A **Non-Clustered Index** has a structure that is separate from the data rows. Its leaf nodes contain the indexed key values along with pointers (row locators) that point to the physical location of the corresponding data rows. A table can have multiple non-clustered indexes. An analogy is the index at the back of a textbook, which lists keywords in alphabetical order and provides page numbers (pointers) to find the actual content.

| Feature                | Clustered Index                                                        | Non-Clustered Index                                                                  |
| ---------------------- | ---------------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| **Number per Table**   | Only one                                                               | Multiple                                                                             |
| **Data Storage**       | Physically sorts and stores the data rows of the table.                | Creates a separate structure with pointers to the data rows.                         |
| **Leaf Nodes Contain** | The actual data rows.                                                  | Index keys and pointers (row locators).                                              |
| **Physical Order**     | Dictates the physical order of rows on disk.                           | Logical order is separate from the physical order of rows.                           |
| **Primary Use Case**   | Range queries, sorting, columns that are frequently accessed in order. | Fast lookups on specific values, covering queries.                                   |
| **Performance Impact** | Faster for reads on the indexed column(s), especially ranges.          | Slower than clustered index for reads (requires an extra lookup step), but flexible. |

### Query Processing & Optimization
When a user submits a query, the DBMS does not execute it blindly. Instead, it undergoes a sophisticated process of optimization to find the most efficient method of execution.
1. **Query Optimizer**: This is the component of the query processor responsible for analyzing a query and generating one or more potential execution plans. It uses statistics about the data (such as table sizes and data distribution) and the available indexes to estimate the "cost" (in terms of I/O, CPU, and memory) of each plan.

2. **Query Execution Plan**: This is the output of the optimizer—a detailed, step-by-step roadmap that the database engine will follow to execute the query. Analyzing the execution plan is the primary method for diagnosing and resolving performance issues.58 Key operators in an execution plan include:
    - **Table Scan**: Reads every row in the table. This is very inefficient for large tables and is often a sign that an index is missing or cannot be used.
    - **Index Seek**: Uses an index to navigate directly to the required rows without scanning the entire table. This is highly efficient.
    - **Join Operations**: The plan specifies the algorithm used to combine rows from multiple tables, such as a Nested Loop Join, a Hash Join, or a Merge Join. The choice of join algorithm can have a massive impact on performance.

![[dbms-query-process.excalidraw.png]]

### Partitioning & Sharding
For very large tables, additional physical storage strategies can be employed to improve manageability and performance.
1. **Partitioning**: This technique involves dividing a single large logical table into smaller, more manageable physical pieces called partitions. For example, a sales table could be partitioned by month or year. Queries that filter on the partition key (e.g., `WHERE sale_date = '2023-10-15'`) can then access only the relevant partition, dramatically reducing the amount of data that needs to be scanned.
2. **Sharding**: This is a form of horizontal partitioning where the data is not just split into different partitions on the same server, but is distributed across multiple independent database servers. Each server holds a "shard" of the data. Sharding is a key technique for achieving massive horizontal scalability, as it distributes both the data and the query load across a cluster of machines.