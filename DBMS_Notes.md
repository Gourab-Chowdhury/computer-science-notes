# 📚 Complete DBMS Notes — Zero to Advanced
### For University Exams | Job Interviews | Placements

---

> **How to use these notes:** Read module by module. Each section has theory, examples, interview tips, and exam-ready summaries. Keywords in **bold** are frequently asked.

---

## 📋 Table of Contents

1. [Module 1 – Introduction to Database Systems](#module-1)
2. [Module 2 – Entity-Relationship (ER) Model](#module-2)
3. [Module 3 – Relational Data Model & Formal Query Languages](#module-3)
4. [Module 4 – SQL: Core to Advanced](#module-4)
5. [Module 5 – Database Design Theory & Normalization](#module-5)
6. [Module 6 – Transaction Management & Concurrency Control](#module-6)
7. [Module 7 – Database Recovery & Security](#module-7)
8. [Module 8 – Storage, Indexing & Query Processing](#module-8)
9. [Module 9 – Distributed & Parallel Databases](#module-9)
10. [Module 10 – NoSQL, NewSQL & Modern Paradigms](#module-10)
11. [Module 11 – Emerging Trends & Advanced Topics](#module-11)
12. [Quick Revision Cheat Sheet](#cheat-sheet)

---

<a name="module-1"></a>
# Module 1: Introduction to Database Systems

---

## 1.1 What is a Database?

A **database** is an organized collection of related data that can be easily accessed, managed, and updated.

Think of it like a **digital filing cabinet** — instead of paper files stored in drawers, data is stored in tables and can be retrieved instantly.

**Examples:**
- A school storing student records
- Amazon storing product and order information
- A hospital storing patient records

---

## 1.2 File-Based System vs. DBMS

Before databases existed, data was stored in **flat files** (like Excel sheets or text files). This had many problems.

| Feature | File-Based System | DBMS |
|---|---|---|
| Data Redundancy | High (same data stored multiple times) | Controlled (minimal duplication) |
| Data Inconsistency | Common (different files have different values) | Avoided |
| Data Sharing | Difficult | Easy (multiple users simultaneously) |
| Security | Poor | Role-based, fine-grained |
| Data Independence | None | High |
| Crash Recovery | Manual | Automatic |
| Query Language | No standard | SQL (powerful, standardized) |

**Example of the problem:**  
A university stores student names in both the "Marks" file and the "Library" file. If a student changes their name, it must be updated in both files manually — this is **data inconsistency**.

---

## 1.3 What is a DBMS?

A **Database Management System (DBMS)** is software that manages databases. It acts as an **interface between users and the database**.

```
User / Application
       ↓
     DBMS  ← (manages access, security, integrity)
       ↓
   Database (actual stored data)
```

**Popular DBMS Software:**
- **Relational:** MySQL, PostgreSQL, Oracle, SQL Server, SQLite
- **NoSQL:** MongoDB, Redis, Cassandra, Neo4j
- **Cloud:** AWS RDS, Google Firestore, Azure Cosmos DB

---

## 1.4 Characteristics of DBMS

### 1. Data Abstraction
DBMS hides the complexity of how data is physically stored. Users see a **simple, clean view** of data.

Three levels of abstraction:
```
┌─────────────────────────────────┐
│   View Level (External)         │  ← What users see (customized views)
├─────────────────────────────────┤
│   Logical Level (Conceptual)    │  ← What data is stored & relationships
├─────────────────────────────────┤
│   Physical Level (Internal)     │  ← How data is physically stored on disk
└─────────────────────────────────┘
```

### 2. Data Independence
Changes at one level do **not affect** other levels.

- **Physical Data Independence:** Changing how data is stored (e.g., moving from HDD to SSD, changing file format) does NOT affect the logical schema or user applications.
- **Logical Data Independence:** Adding a new column to a table does NOT break existing user views or applications.

> 💡 **Interview Tip:** Logical data independence is harder to achieve than physical data independence.

### 3. Data Sharing
Multiple users can access the database **simultaneously** without conflict (handled via concurrency control).

### 4. Data Integrity
DBMS enforces rules to keep data **accurate and consistent**:
- Age must be a positive number
- A student's department must exist in the department table

### 5. Data Security
Only **authorized users** can access specific data. Example: A student can view their own marks but not change them.

### 6. Data Redundancy Control
DBMS minimizes duplication through **normalization** and centralized storage.

### 7. Backup and Recovery
DBMS automatically creates backups and can restore data after a crash.

---

## 1.5 Database Users and Roles

| User Type | Description | Example |
|---|---|---|
| **DBA (Database Administrator)** | Manages the DBMS — security, backup, performance tuning, user access | Senior database engineer |
| **Application Programmers** | Write code that interacts with the DB | Backend developers using Java/Python |
| **Sophisticated End Users** | Write complex queries directly | Data analysts using SQL |
| **Naive End Users** | Use apps that interact with DB (don't know SQL) | Bank customers using ATM |
| **System Analysts** | Determine requirements and design the system | Business analysts |

---

## 1.6 Data Models

A **data model** defines how data is structured, related, and constrained.

### 1. Hierarchical Model
Data is organized in a **tree structure** (parent-child relationship). Each child has only one parent.

```
        University
           |
    ┌──────┴──────┐
  Science       Arts
    |              |
  Physics      History
```

- **Advantage:** Fast for hierarchical data
- **Disadvantage:** Rigid, can't handle many-to-many relationships
- **Example:** IBM IMS (old banking systems)

### 2. Network Model
Like hierarchical but allows **multiple parents** for a child (graph structure).

- **Advantage:** Flexible, handles M:N relationships
- **Disadvantage:** Very complex to navigate, requires knowledge of physical structure
- **Example:** IDS, IDMS

### 3. Relational Model (Most Important ⭐)
Data stored in **tables (relations)**. Relationships through **keys**.

```
Students Table:
| RollNo | Name    | Dept |
|--------|---------|------|
| 101    | Aryan   | CS   |
| 102    | Priya   | IT   |
```

- **Advantage:** Simple, flexible, powerful SQL
- **Disadvantage:** Not ideal for complex hierarchical data
- **Used by:** MySQL, PostgreSQL, Oracle

### 4. Object-Oriented Model
Data stored as **objects** (like in OOP programming). Supports inheritance, encapsulation.
- **Used by:** ObjectDB, db4o
- **Good for:** Complex data like multimedia, CAD

### 5. Semi-Structured Model
Data doesn't follow a strict schema. Uses formats like **JSON and XML**.
- **Used by:** MongoDB (documents), CouchDB
- **Good for:** Flexible, rapidly changing data structures

---

## 1.7 Database Languages

| Language | Full Form | Purpose | Examples |
|---|---|---|---|
| **DDL** | Data Definition Language | Define/modify structure | CREATE, ALTER, DROP, TRUNCATE, RENAME, COMMENT |
| **DML** | Data Manipulation Language | Insert/update/delete/retrieve data | INSERT, UPDATE, DELETE, SELECT |
| **DCL** | Data Control Language | Control access/permissions | GRANT, REVOKE |
| **TCL** | Transaction Control Language | Manage transactions | COMMIT, ROLLBACK, SAVEPOINT |

---

## 1.8 DBMS Architecture

### 2-Tier Architecture
```
Client (Application) ←→ Database Server
```
- Direct connection between client and DB
- **Simple, fast** but not scalable
- Example: Desktop application connecting directly to MySQL

### 3-Tier Architecture
```
Client (Browser/App) ←→ Application Server ←→ Database Server
```
- **Most common** in modern web applications
- Application server handles business logic
- Example: Web browser → Node.js server → PostgreSQL

### Client-Server Architecture
Clients send requests; the server processes them and returns results.

### Centralized vs. Distributed
- **Centralized:** All data on one server. Simple but single point of failure.
- **Distributed:** Data spread across multiple servers/locations. More complex but scalable and fault-tolerant.

---

## 1.9 Instances vs. Schemas

| Term | Meaning | Analogy |
|---|---|---|
| **Schema** | The structure/design of the database (table names, column names, data types) | Blueprint of a house |
| **Instance** | The actual data stored in the database at a particular moment | The house built from the blueprint |

```sql
-- Schema: defines structure
CREATE TABLE Student (
  RollNo INT PRIMARY KEY,
  Name VARCHAR(50),
  Age INT
);

-- Instance: actual data at time T
| RollNo | Name  | Age |
|--------|-------|-----|
| 101    | Aryan | 20  |
```

> 🔑 **Key Point:** Schema rarely changes. Instance changes every time data is inserted/updated/deleted.

---

## Module 1 — Quick Summary

- DBMS = software to manage databases efficiently
- Solves problems of file systems: redundancy, inconsistency, poor security
- Three levels of abstraction: Physical → Logical → View
- Two types of data independence: Physical and Logical
- Data models: Hierarchical, Network, Relational (most important), OO, Semi-structured
- Languages: DDL, DML, DCL, TCL
- Architecture: 2-tier, 3-tier, Client-Server, Centralized vs Distributed

---

<a name="module-2"></a>
# Module 2: Entity-Relationship (ER) Model

---

## 2.1 What is the ER Model?

The **Entity-Relationship (ER) Model** is a **conceptual data model** used to design databases at a high level before actual implementation. It uses diagrams (ER Diagrams) to visually represent:
- What data exists (**entities**)
- What properties data has (**attributes**)
- How data is related (**relationships**)

Think of an ER diagram as the **architect's blueprint** before building the database.

---

## 2.2 Entities and Entity Sets

An **entity** is a real-world object or concept that has existence.

- **Strong Entity:** Has its own primary key. Can exist independently.
  - Example: `Student`, `Employee`, `Product`
- **Weak Entity:** Does NOT have its own primary key. Depends on a strong entity.
  - Example: `Dependent` (of an Employee), `Order_Item` (of an Order)

An **entity set** is a collection of similar entities.
- Example: All students in a university = `Student` entity set

**ER Notation:**
```
Strong Entity  → Rectangle  [ Student ]
Weak Entity    → Double Rectangle  [[ Dependent ]]
```

---

## 2.3 Attributes

Attributes are **properties** of an entity.

| Type | Description | Example | Notation |
|---|---|---|---|
| **Simple** | Cannot be divided further | Age, RollNo | Oval |
| **Composite** | Can be divided into sub-parts | Name (First + Last) | Oval with sub-ovals |
| **Multivalued** | Can have multiple values | Phone_Numbers, Skills | Double Oval |
| **Derived** | Calculated from other attributes | Age (from DOB) | Dashed Oval |
| **Key Attribute** | Uniquely identifies an entity | RollNo, StudentID | Underlined in oval |
| **Null** | Can have no value | Middle_Name | — |

**Example:**
```
Student Entity Attributes:
- RollNo (Key) — uniquely identifies
- Name (Composite) → First_Name + Last_Name
- Phone (Multivalued) → can have multiple phones
- Age (Derived) → calculated from DOB
- DOB (Simple)
- Address (Composite) → Street + City + State + ZIP
```

---

## 2.4 Relationships and Relationship Sets

A **relationship** is an association between two or more entities.

**Example:** Student **enrolls in** Course → "Enrolls_In" is the relationship.

A **relationship set** is a collection of similar relationships.

**Degree of a Relationship:**
- **Unary (Recursive):** Entity relates to itself. Example: Employee *manages* Employee
- **Binary:** Two entities. Example: Student *enrolls* in Course (most common)
- **Ternary:** Three entities. Example: Doctor *prescribes* Medicine to Patient

---

## 2.5 Cardinality (Mapping Constraints)

Cardinality defines **how many entities** on one side relate to entities on the other side.

### One-to-One (1:1)
One entity in A is related to **at most one** entity in B.
```
Person ——1—— has ——1—— Passport
(One person has one passport)
```

### One-to-Many (1:N)
One entity in A is related to **many** entities in B.
```
Department ——1—— employs ——N—— Employees
(One department has many employees)
```

### Many-to-Many (M:N)
Many entities in A relate to **many** entities in B.
```
Students ——M—— enroll ——N—— Courses
(Many students enroll in many courses)
```

---

## 2.6 Participation Constraints

**Total Participation (Mandatory):** Every entity MUST participate in the relationship.
- Shown as **double line** in ER diagram
- Example: Every employee MUST work for a department

**Partial Participation (Optional):** Some entities may not participate.
- Shown as **single line**
- Example: Not every employee manages a project

```
Department ══════ employs ————— Employee
    (total)                   (partial)
Every dept has employees, but not every employee is a manager.
```

---

## 2.7 Weak Entities

A **weak entity** cannot be uniquely identified by its own attributes alone. It depends on a **strong (owner) entity** through an **identifying relationship**.

Key concepts:
- Weak entity has a **partial key (discriminator)** — underlined with dashed line
- Its full key = Partial Key + Primary Key of owner entity
- The identifying relationship is shown with **double diamond**

**Example:**
```
Employee [[ Dependent ]]
   |            |
   ══ has_dep ══
   
Dependent's key = EmpID (from Employee) + Dep_Name (partial key)
```

---

## 2.8 Extended ER (EER) Model

The EER model adds more semantic richness to the basic ER model.

### Specialization
**Top-down** approach. We take a general entity and divide it into **specialized sub-entities**.

```
        Person
       /      \
  Employee   Student
  /    \
Manager Engineer
```

- **Disjoint (d):** An entity can belong to only ONE subclass (Employee is either Manager OR Engineer, not both)
- **Overlapping (o):** An entity can belong to MULTIPLE subclasses (a person can be both a Student AND an Employee)

### Generalization
**Bottom-up** approach. We combine multiple entities into a **general entity**.

```
Car + Truck + Bus → Vehicle
```

Think of it as the reverse of specialization.

### Aggregation
When a relationship participates in another relationship.

**Problem:** ER can't directly model "a relationship related to another relationship."

**Solution:** Treat the relationship as an entity (aggregate it).

```
Example: An Employee works_on a Project
         → This work is evaluated by a Manager
         
[Employee] — works_on — [Project]
         ↘_aggregated_↗
                |
           evaluated_by
                |
           [Manager]
```

### Inheritance
Subclasses **inherit** all attributes and relationships of the superclass.
- Manager inherits all attributes of Employee
- Additional attributes can be added in subclass

---

## 2.9 ER Diagram Notations

### Chen Notation (Original)

| Symbol | Represents |
|---|---|
| Rectangle | Entity |
| Double Rectangle | Weak Entity |
| Ellipse/Oval | Attribute |
| Double Ellipse | Multivalued Attribute |
| Dashed Ellipse | Derived Attribute |
| Underlined in Oval | Key Attribute |
| Diamond | Relationship |
| Double Diamond | Identifying Relationship (for weak entity) |
| Single Line | Partial Participation |
| Double Line | Total Participation |
| 1, N, M on lines | Cardinality |

### Crow's Foot Notation (Used in tools like MySQL Workbench, Lucidchart)

| Symbol | Meaning |
|---|---|
| `|—|` | One and only one (mandatory 1:1) |
| `|—<` | One to many |
| `o—<` | Zero or many |
| `o—|` | Zero or one |

---

## 2.10 Mapping ER/EER to Relational Schema

### Strong Entity → Table
Each strong entity becomes a table. Its key attribute becomes the **primary key**.

```
Entity: Student(RollNo, Name, Age)
Table:  Student(RollNo PK, Name, Age)
```

### Composite Attribute → Flat Columns
Break composite attributes into simple columns.
```
Name (First, Last) → First_Name, Last_Name as separate columns
```

### Multivalued Attribute → Separate Table
```
Student_Phone(RollNo FK, PhoneNumber)
PK = (RollNo, PhoneNumber)
```

### Weak Entity → Table with Owner's Key
```
Dependent(EmpID FK, Dep_Name, Relationship)
PK = (EmpID, Dep_Name)
```

### 1:1 Relationship → Add FK to either table (usually the total participation side)
```
Employee(EmpID, Name, PassportNo FK)
Passport(PassportNo PK, ExpiryDate)
```

### 1:N Relationship → Add FK to the "N" side
```
Department(DeptID PK, DeptName)
Employee(EmpID PK, Name, DeptID FK)
                            ↑ references Department
```

### M:N Relationship → Create a new junction/bridge table
```
Student(RollNo PK, Name)
Course(CourseID PK, CourseName)
Enrollment(RollNo FK, CourseID FK, EnrollDate)
           PK = (RollNo, CourseID)
```

### Specialization/Generalization → Three Approaches
1. **Single table for all:** One table with NULLs for non-applicable columns
2. **Table per subclass + superclass:** Most common, preferred
3. **Table per subclass only:** Repeat superclass attributes in each subclass table

---

## 2.11 Real-World ER Design Examples

### University ER Design
**Entities:** Student, Professor, Course, Department, Classroom

**Key Relationships:**
- Student ENROLLS_IN Course (M:N)
- Professor TEACHES Course (1:N)
- Course BELONGS_TO Department (N:1)
- Student BELONGS_TO Department (N:1)

### Hospital ER Design
**Entities:** Patient, Doctor, Ward, Medicine, Appointment

**Key Relationships:**
- Patient HAS Appointment with Doctor (M:N)
- Doctor WORKS_IN Department (N:1)
- Doctor PRESCRIBES Medicine to Patient (Ternary)
- Patient ADMITTED_TO Ward (M:1)

---

## Module 2 — Quick Summary

- ER Model = blueprint for database design
- Entity (strong/weak), Attribute (simple/composite/multivalued/derived), Relationship
- Cardinality: 1:1, 1:N, M:N
- Participation: Total (mandatory) vs Partial (optional)
- EER adds: Specialization, Generalization, Aggregation, Inheritance
- Mapping rules: Strong entity→table, M:N→junction table, Multivalued attr→separate table

---

<a name="module-3"></a>
# Module 3: Relational Data Model & Formal Query Languages

---

## 3.1 Structure of a Relational Database

The relational model organizes data into **relations (tables)**.

**Terminology:**

| Relational Term | Common Synonym | Description |
|---|---|---|
| **Relation** | Table | A 2D structure with rows and columns |
| **Tuple** | Row / Record | One instance of data |
| **Attribute** | Column / Field | A property of the relation |
| **Domain** | Data type | Set of valid values for an attribute |
| **Degree** | Arity | Number of attributes in a relation |
| **Cardinality** | — | Number of tuples in a relation |

**Example:**
```
Student Relation (Degree=3, Cardinality=3):

| RollNo | Name    | Dept |   ← Attributes (3 = Degree)
|--------|---------|------|
| 101    | Aryan   | CS   |   ← Tuple 1
| 102    | Priya   | IT   |   ← Tuple 2
| 103    | Rahul   | CS   |   ← Tuple 3
                              ↑ Cardinality = 3
```

**Properties of a Relation:**
1. No duplicate tuples (each row is unique)
2. Tuples are unordered (order doesn't matter)
3. Attributes are atomic (no multivalued attributes in one cell — 1NF)
4. Each attribute has a unique name
5. Attribute values belong to the defined domain

---

## 3.2 Keys in Relational Model

Keys are used to **uniquely identify tuples** in a relation.

### Super Key
Any set of attributes that **uniquely identifies** a tuple.
- Can have extra (unnecessary) attributes
- Example: {RollNo}, {RollNo, Name}, {RollNo, Name, Dept} — all are super keys if RollNo is unique

### Candidate Key
A **minimal super key** — no attribute can be removed while still maintaining uniqueness.
- A relation can have **multiple candidate keys**
- Example: {RollNo} and {Email} are both candidate keys if both are unique

### Primary Key (PK)
The **chosen** candidate key to uniquely identify tuples.
- Cannot be NULL
- Cannot be duplicate
- Only ONE primary key per table

### Alternate Key
Candidate keys that were **NOT chosen** as the primary key.

### Foreign Key (FK)
An attribute in one table that **references the primary key** of another table.
- Used to **link tables** together
- Enforces **referential integrity**

```
Department(DeptID PK, DeptName)
Employee(EmpID PK, Name, DeptID FK → Department.DeptID)
```

### Composite Key
A primary key made of **two or more attributes**.
```
Enrollment(RollNo, CourseID, Grade)
PK = (RollNo, CourseID) ← composite key
```

### Surrogate Key
An **artificial key** added when there's no natural primary key.
- Usually auto-incremented integers
- Example: `id SERIAL PRIMARY KEY` in PostgreSQL

---

## 3.3 Integrity Constraints

Rules that ensure **accuracy and consistency** of data.

### 1. Entity Integrity
**Primary key cannot be NULL.**

```sql
-- This would VIOLATE entity integrity:
INSERT INTO Student VALUES (NULL, 'Aryan', 'CS'); -- ❌ RollNo can't be NULL
```

### 2. Referential Integrity
A **foreign key value** must either be NULL or match an existing primary key in the referenced table.

```sql
-- Employee's DeptID must exist in Department table
INSERT INTO Employee VALUES (201, 'Priya', 99);
-- ❌ If DeptID=99 doesn't exist in Department → Referential Integrity Violation
```

**Actions on FK violation:**
- `CASCADE` → Automatically delete/update child records
- `SET NULL` → Set FK to NULL
- `SET DEFAULT` → Set FK to default value
- `RESTRICT / NO ACTION` → Reject the operation

### 3. Domain Constraint
Attribute values must belong to the **defined domain** (data type and range).

```sql
Age INT CHECK (Age > 0 AND Age < 150)  -- domain constraint
Gender CHAR(1) CHECK (Gender IN ('M', 'F', 'O'))
```

### 4. Key Constraint
Primary key must be **unique and not null**.

### 5. Assertions (General Constraints)
Complex constraints that span multiple tables.

```sql
-- Example: No employee can earn more than their manager
CREATE ASSERTION salary_check
CHECK (NOT EXISTS (
  SELECT * FROM Employee E, Employee M
  WHERE E.ManagerID = M.EmpID AND E.Salary > M.Salary
));
```

---

## 3.4 Relational Algebra

Relational algebra is a **formal procedural query language** — you specify HOW to get the data step by step.

It forms the **theoretical foundation of SQL**.

### Basic Operations

#### 1. Selection (σ) — Filter Rows
Selects tuples that satisfy a condition.

```
Notation:  σ_condition(Relation)
SQL equiv: WHERE clause

Example:   σ_Dept='CS'(Student)
→ Returns all students in CS department
```

#### 2. Projection (π) — Filter Columns
Selects specific attributes (columns).

```
Notation:  π_attr1,attr2,...(Relation)
SQL equiv: SELECT columns

Example:   π_Name,Dept(Student)
→ Returns only Name and Dept columns
```

#### 3. Union (∪)
Combines tuples from two **compatible** relations (same degree, compatible domains).

```
Notation:  R ∪ S
SQL equiv: UNION

Example:   CS_Students ∪ IT_Students
→ All students from either department (no duplicates)
```

#### 4. Intersection (∩)
Returns tuples that exist in **both** relations.

```
Notation:  R ∩ S
SQL equiv: INTERSECT

Example:   Employees_Delhi ∩ Senior_Employees
→ Senior employees who are in Delhi
```

#### 5. Set Difference (−)
Returns tuples in R that are **NOT in S**.

```
Notation:  R − S
SQL equiv: EXCEPT / MINUS

Example:   All_Students − Enrolled_Students
→ Students who have NOT enrolled in any course
```

#### 6. Cartesian Product (×)
Combines every tuple of R with every tuple of S.

```
Notation:  R × S
SQL equiv: FROM R, S (without WHERE)

If R has 3 tuples and S has 4 tuples → Result has 3×4 = 12 tuples
```

#### 7. Renaming (ρ)
Renames a relation or its attributes.

```
Notation:  ρ_NewName(Relation)
           ρ_NewName(A1,A2,...)(Relation)

Example:   ρ_Emp(ID, Name)(Employee)
```

### Join Operations (Most Important ⭐)

#### Theta Join (θ)
Cartesian product + selection condition.

```
R ⋈_(R.A θ S.B) S
where θ is a comparison operator (=, <, >, ≤, ≥, ≠)
```

#### Equi-Join
Special theta join where condition is equality (=).

```
Employee ⋈_(Employee.DeptID = Department.DeptID) Department
```

#### Natural Join (⋈)
Equi-join that **automatically joins on common attribute names** and removes duplicate columns.

```
Employee ⋈ Department
→ Joins on DeptID (common column), removes one copy of DeptID
```

#### Outer Joins
Includes tuples that do NOT have matching tuples (filled with NULLs).

```
Left Outer Join  (⟕): All tuples from LEFT + matching from right
Right Outer Join (⟖): All tuples from RIGHT + matching from left
Full Outer Join  (⟗): All tuples from BOTH sides
```

**Example:**
```
Employee:                   Department:
EmpID  DeptID               DeptID  DeptName
101    10                   10      CS
102    20                   20      IT
103    NULL (no dept)       30      HR (no employees)

LEFT OUTER JOIN (Employee ⟕ Department):
101  10  CS
102  20  IT
103  NULL NULL  ← employee with no dept still shown

RIGHT OUTER JOIN:
101  10   CS
102  20   IT
NULL NULL  HR  ← dept with no employee still shown

FULL OUTER JOIN:
101  10  CS
102  20  IT
103  NULL NULL
NULL NULL HR
```

#### Division (÷)
Used for "for all" type queries.

```
R ÷ S = tuples in R that appear with ALL tuples of S

Example: Find students enrolled in ALL courses
Enrollment ÷ Course
→ Returns students who have enrolled in every course
```

---

## 3.5 Relational Calculus

Relational calculus is a **non-procedural** (declarative) query language — you specify WHAT you want, not HOW to get it.

### Tuple Relational Calculus (TRC)
Queries expressed in terms of **tuples**.

```
Notation: {t | condition(t)}
"The set of tuples t such that condition(t) is true"

Example: Find name of all CS students
{t.Name | Student(t) AND t.Dept = 'CS'}

Example: Find students who enrolled in course C101
{t | Student(t) AND ∃e (Enrollment(e) AND e.RollNo = t.RollNo AND e.CourseID = 'C101')}
```

**Quantifiers used:**
- **∃ (There exists):** At least one tuple satisfies
- **∀ (For all):** All tuples must satisfy

### Domain Relational Calculus (DRC)
Queries expressed in terms of **domain variables** (individual column values).

```
Notation: {<x1, x2, ...> | condition}

Example: Find names of CS students
{<n> | ∃r, d (Student(r, n, d) AND d = 'CS')}
where r=RollNo, n=Name, d=Dept
```

### Comparison: RA vs TRC vs DRC

| Feature | Relational Algebra | TRC | DRC |
|---|---|---|---|
| Type | Procedural | Non-procedural | Non-procedural |
| Based on | Operations on sets | First-order logic (tuples) | First-order logic (domains) |
| SQL closer to | — | TRC | — |
| Expressiveness | Equivalent (all are equally expressive) | = | = |

> 💡 **Interview Tip:** All three are **relationally complete** — they can express the same set of queries. SQL is based on relational calculus concepts but has procedural elements too.

---

## 3.6 Equivalence Rules in Relational Algebra

These rules are used in **query optimization**:

1. σ_c1 AND c2(R) = σ_c1(σ_c2(R)) — **Cascade of selection**
2. σ_c1(σ_c2(R)) = σ_c2(σ_c1(R)) — **Commutativity of selection**
3. π_L1(π_L2(R)) = π_L1(R) if L1 ⊆ L2 — **Cascade of projection**
4. R ⋈ S = S ⋈ R — **Commutativity of join**
5. (R ⋈ S) ⋈ T = R ⋈ (S ⋈ T) — **Associativity of join**
6. σ_c(R ⋈ S) = σ_c(R) ⋈ S if c involves only R's attributes — **Push selection below join**

---

## Module 3 — Quick Summary

- Relations have: tuples (rows), attributes (columns), domains (valid values)
- Key hierarchy: Super key → Candidate key → Primary key (chosen one)
- Foreign key enforces referential integrity between tables
- Relational Algebra: Selection(σ), Projection(π), Union, Intersect, Set-diff, Cartesian(×), Join(⋈), Division(÷)
- Join types: Theta, Equi, Natural, Left/Right/Full Outer
- TRC and DRC are non-procedural alternatives to RA
- All three (RA, TRC, DRC) are equally expressive (relationally complete)

<a name="module-4"></a>
# Module 4: Structured Query Language (SQL) — Core to Advanced

---

## 4.1 What is SQL?

**SQL (Structured Query Language)** is the standard language to interact with relational databases.

- Developed by IBM in the 1970s (originally called SEQUEL)
- Standardized by ANSI/ISO
- Declarative: you say WHAT you want, not HOW to get it

---

## PART A: Basic SQL

---

## 4.2 DDL — Data Definition Language

### CREATE TABLE
```sql
CREATE TABLE Student (
  RollNo    INT           PRIMARY KEY,
  Name      VARCHAR(100)  NOT NULL,
  Age       INT           CHECK (Age BETWEEN 15 AND 35),
  Dept      VARCHAR(50)   DEFAULT 'Undecided',
  Email     VARCHAR(100)  UNIQUE,
  JoinDate  DATE          DEFAULT CURRENT_DATE
);
```

**Constraints inline:**
```sql
CREATE TABLE Enrollment (
  RollNo    INT,
  CourseID  VARCHAR(10),
  Grade     CHAR(2),
  PRIMARY KEY (RollNo, CourseID),                        -- composite PK
  FOREIGN KEY (RollNo) REFERENCES Student(RollNo)        -- FK
    ON DELETE CASCADE                                    -- cascade delete
    ON UPDATE CASCADE,
  FOREIGN KEY (CourseID) REFERENCES Course(CourseID)
    ON DELETE RESTRICT
);
```

### ALTER TABLE
```sql
-- Add a column
ALTER TABLE Student ADD COLUMN Phone VARCHAR(15);

-- Drop a column
ALTER TABLE Student DROP COLUMN Phone;

-- Rename a column (PostgreSQL)
ALTER TABLE Student RENAME COLUMN Name TO StudentName;

-- Modify data type
ALTER TABLE Student ALTER COLUMN Age TYPE SMALLINT;  -- PostgreSQL
ALTER TABLE Student MODIFY Age SMALLINT;             -- MySQL

-- Add constraint
ALTER TABLE Student ADD CONSTRAINT chk_age CHECK (Age > 0);

-- Drop constraint
ALTER TABLE Student DROP CONSTRAINT chk_age;
```

### DROP vs TRUNCATE vs DELETE

| Command | Removes | Rollback? | Resets Auto-increment? |
|---|---|---|---|
| `DROP TABLE` | Entire table (structure + data) | No (DDL) | N/A (table gone) |
| `TRUNCATE TABLE` | All rows (keeps structure) | No (DDL) | Yes |
| `DELETE FROM` | Specific/all rows | Yes (DML) | No |

```sql
DROP TABLE Student;         -- deletes table completely
TRUNCATE TABLE Student;     -- deletes all rows, keeps table
DELETE FROM Student;        -- deletes all rows (slower, logged)
```

### CREATE INDEX
```sql
CREATE INDEX idx_dept ON Student(Dept);
CREATE UNIQUE INDEX idx_email ON Student(Email);

-- Drop index
DROP INDEX idx_dept;
```

---

## 4.3 DML — Data Manipulation Language

### INSERT
```sql
-- Insert single row
INSERT INTO Student (RollNo, Name, Age, Dept)
VALUES (101, 'Aryan', 20, 'CS');

-- Insert multiple rows
INSERT INTO Student VALUES
  (102, 'Priya', 21, 'IT', 'priya@email.com', DEFAULT),
  (103, 'Rahul', 22, 'CS', 'rahul@email.com', DEFAULT);

-- Insert from another table
INSERT INTO CS_Students
SELECT * FROM Student WHERE Dept = 'CS';
```

### UPDATE
```sql
-- Update specific rows
UPDATE Student
SET Age = 21, Dept = 'CS'
WHERE RollNo = 101;

-- Update using another table
UPDATE Employee e
SET Salary = Salary * 1.10
WHERE DeptID = (SELECT DeptID FROM Department WHERE DeptName = 'CS');
```

### DELETE
```sql
-- Delete specific rows
DELETE FROM Student WHERE RollNo = 101;

-- Delete with subquery
DELETE FROM Student
WHERE RollNo IN (SELECT RollNo FROM Enrollment WHERE Grade = 'F');

-- Delete all rows
DELETE FROM Student;
```

### MERGE (Upsert)
```sql
-- PostgreSQL: INSERT ... ON CONFLICT
INSERT INTO Student (RollNo, Name, Age)
VALUES (101, 'Aryan Updated', 22)
ON CONFLICT (RollNo)
DO UPDATE SET Name = EXCLUDED.Name, Age = EXCLUDED.Age;
```

---

## 4.4 Basic SELECT Queries

### Fundamental Structure
```sql
SELECT [DISTINCT] column1, column2, ...
FROM   table_name
WHERE  condition
GROUP BY column
HAVING group_condition
ORDER BY column [ASC|DESC]
LIMIT n OFFSET m;
```

**Order of Execution (important for exams!):**
```
FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY → LIMIT
```

### Examples

```sql
-- Select all columns
SELECT * FROM Student;

-- Select specific columns
SELECT Name, Dept FROM Student;

-- With alias
SELECT Name AS StudentName, Dept AS Department FROM Student;

-- Remove duplicates
SELECT DISTINCT Dept FROM Student;

-- Filter with WHERE
SELECT * FROM Student WHERE Dept = 'CS' AND Age > 20;

-- Pattern matching with LIKE
SELECT * FROM Student WHERE Name LIKE 'A%';     -- starts with A
SELECT * FROM Student WHERE Name LIKE '%ar%';   -- contains 'ar'
SELECT * FROM Student WHERE Name LIKE '_ryan';  -- second char r

-- NULL handling
SELECT * FROM Student WHERE Phone IS NULL;
SELECT * FROM Student WHERE Phone IS NOT NULL;

-- BETWEEN (inclusive)
SELECT * FROM Student WHERE Age BETWEEN 18 AND 25;

-- IN operator
SELECT * FROM Student WHERE Dept IN ('CS', 'IT', 'ECE');

-- ORDER BY
SELECT * FROM Student ORDER BY Age DESC, Name ASC;

-- LIMIT and OFFSET (pagination)
SELECT * FROM Student ORDER BY RollNo LIMIT 10 OFFSET 20;  -- page 3
```

### Aggregate Functions
```sql
SELECT COUNT(*)         FROM Student;                      -- count all rows
SELECT COUNT(Phone)     FROM Student;                      -- count non-NULLs
SELECT COUNT(DISTINCT Dept) FROM Student;                  -- distinct depts
SELECT SUM(Salary)      FROM Employee;
SELECT AVG(Salary)      FROM Employee;
SELECT MAX(Age)         FROM Student;
SELECT MIN(Age)         FROM Student;
```

### GROUP BY and HAVING
```sql
-- Students per department
SELECT Dept, COUNT(*) AS StudentCount
FROM Student
GROUP BY Dept;

-- Departments with more than 50 students
SELECT Dept, COUNT(*) AS StudentCount
FROM Student
GROUP BY Dept
HAVING COUNT(*) > 50;

-- Average salary by department, only depts with avg > 50000
SELECT DeptID, AVG(Salary) AS AvgSalary
FROM Employee
GROUP BY DeptID
HAVING AVG(Salary) > 50000
ORDER BY AvgSalary DESC;
```

> 💡 **Exam Tip:** `WHERE` filters individual rows (before grouping). `HAVING` filters groups (after GROUP BY). You **cannot** use aggregate functions in WHERE.

---

## PART B: Intermediate & Advanced SQL

---

## 4.5 Joins

```sql
-- Sample tables
-- Employee(EmpID, Name, DeptID, ManagerID)
-- Department(DeptID, DeptName, Location)
```

### INNER JOIN
Returns rows where there is a **match in both tables**.

```sql
SELECT e.Name, d.DeptName
FROM Employee e
INNER JOIN Department d ON e.DeptID = d.DeptID;
```

### LEFT OUTER JOIN
Returns **all rows from left table** + matching rows from right.

```sql
SELECT e.Name, d.DeptName
FROM Employee e
LEFT JOIN Department d ON e.DeptID = d.DeptID;
-- Employees with no department → DeptName = NULL
```

### RIGHT OUTER JOIN
Returns **all rows from right table** + matching rows from left.

```sql
SELECT e.Name, d.DeptName
FROM Employee e
RIGHT JOIN Department d ON e.DeptID = d.DeptID;
-- Departments with no employees → Name = NULL
```

### FULL OUTER JOIN
Returns **all rows from both tables**.

```sql
SELECT e.Name, d.DeptName
FROM Employee e
FULL OUTER JOIN Department d ON e.DeptID = d.DeptID;
```

### CROSS JOIN
Returns **Cartesian product** of both tables.

```sql
SELECT e.Name, d.DeptName
FROM Employee e
CROSS JOIN Department d;
-- If Employee has 100 rows and Department has 5 → 500 rows returned
```

### SELF JOIN
A table joined with **itself**.

```sql
-- Find employees and their managers
SELECT e.Name AS Employee, m.Name AS Manager
FROM Employee e
JOIN Employee m ON e.ManagerID = m.EmpID;
```

---

## 4.6 Subqueries

A query **nested inside** another query.

### Simple Subquery (in WHERE)
```sql
-- Find students in the same dept as Aryan
SELECT Name FROM Student
WHERE Dept = (SELECT Dept FROM Student WHERE Name = 'Aryan');
```

### IN with Subquery
```sql
-- Find employees in departments in Bangalore
SELECT Name FROM Employee
WHERE DeptID IN (SELECT DeptID FROM Department WHERE Location = 'Bangalore');
```

### Correlated Subquery
The inner query **depends on the outer query** — executed once per row.

```sql
-- Find employees who earn more than their dept average
SELECT e1.Name, e1.Salary
FROM Employee e1
WHERE e1.Salary > (
  SELECT AVG(e2.Salary)
  FROM Employee e2
  WHERE e2.DeptID = e1.DeptID  -- ← depends on outer query's current row
);
```

### EXISTS
Returns true if subquery returns **at least one row**.

```sql
-- Find departments that have at least one employee
SELECT DeptName FROM Department d
WHERE EXISTS (
  SELECT 1 FROM Employee e WHERE e.DeptID = d.DeptID
);
```

### NOT EXISTS
```sql
-- Find departments with NO employees
SELECT DeptName FROM Department d
WHERE NOT EXISTS (
  SELECT 1 FROM Employee e WHERE e.DeptID = d.DeptID
);
```

### ANY / ALL
```sql
-- Salary greater than at least one IT employee
SELECT Name FROM Employee
WHERE Salary > ANY (SELECT Salary FROM Employee WHERE DeptID = 10);

-- Salary greater than ALL IT employees
SELECT Name FROM Employee
WHERE Salary > ALL (SELECT Salary FROM Employee WHERE DeptID = 10);
```

### Scalar Subquery (in SELECT)
```sql
SELECT Name, 
       (SELECT DeptName FROM Department d WHERE d.DeptID = e.DeptID) AS DeptName
FROM Employee e;
```

---

## 4.7 Set Operations

```sql
-- UNION: combines results, removes duplicates
SELECT Name FROM Student_CS
UNION
SELECT Name FROM Student_IT;

-- UNION ALL: combines results, keeps duplicates (faster)
SELECT Name FROM Student_CS
UNION ALL
SELECT Name FROM Student_IT;

-- INTERSECT: only rows in BOTH
SELECT RollNo FROM CS_Students
INTERSECT
SELECT RollNo FROM Scholarship_Recipients;

-- EXCEPT / MINUS: rows in first but NOT in second
SELECT RollNo FROM All_Students
EXCEPT
SELECT RollNo FROM Enrolled_Students;
```

---

## 4.8 Views

A **view** is a virtual table based on a SELECT query.

```sql
-- Create a view
CREATE VIEW CS_Students AS
SELECT RollNo, Name, Age
FROM Student
WHERE Dept = 'CS';

-- Query the view
SELECT * FROM CS_Students WHERE Age > 20;

-- Update through view (if updatable)
UPDATE CS_Students SET Age = 21 WHERE RollNo = 101;

-- Drop view
DROP VIEW CS_Students;
```

**Benefits of Views:**
1. **Security:** Hide sensitive columns (e.g., salary) from certain users
2. **Simplicity:** Complex queries written once, reused simply
3. **Logical Independence:** If table structure changes, update only the view

**Materialized View:**
Unlike regular views, materialized views **store the query result physically**.

```sql
-- PostgreSQL materialized view
CREATE MATERIALIZED VIEW dept_stats AS
SELECT DeptID, COUNT(*) as emp_count, AVG(Salary) as avg_sal
FROM Employee
GROUP BY DeptID;

-- Refresh when underlying data changes
REFRESH MATERIALIZED VIEW dept_stats;
```

---

## 4.9 SQL Functions

### String Functions
```sql
SELECT UPPER('hello');              -- HELLO
SELECT LOWER('WORLD');              -- world
SELECT LENGTH('Database');          -- 8
SELECT SUBSTRING('Database', 1, 4); -- Data
SELECT TRIM('  hello  ');           -- hello
SELECT REPLACE('Hello World', 'World', 'DB'); -- Hello DB
SELECT CONCAT('Hello', ' ', 'World');  -- Hello World
SELECT LEFT('Database', 4);         -- Data
SELECT RIGHT('Database', 4);        -- base
SELECT LPAD('42', 5, '0');          -- 00042
```

### Numeric Functions
```sql
SELECT ABS(-15);         -- 15
SELECT CEIL(4.3);        -- 5
SELECT FLOOR(4.9);       -- 4
SELECT ROUND(4.567, 2);  -- 4.57
SELECT MOD(17, 5);       -- 2
SELECT POWER(2, 10);     -- 1024
SELECT SQRT(144);        -- 12
```

### Date Functions
```sql
SELECT CURRENT_DATE;                       -- today's date
SELECT CURRENT_TIMESTAMP;                  -- now
SELECT EXTRACT(YEAR FROM '2024-06-15');    -- 2024
SELECT DATE_PART('month', CURRENT_DATE);  -- current month number
SELECT AGE('2000-05-15');                  -- age from DOB
SELECT NOW() + INTERVAL '30 days';        -- 30 days from now
SELECT TO_CHAR(NOW(), 'YYYY-MM-DD');       -- formatted date string
```

### Window Functions (Advanced ⭐)
Window functions perform calculations **across related rows** without collapsing them (unlike GROUP BY).

```sql
-- ROW_NUMBER: assign sequential number to each row
SELECT Name, Salary, Dept,
       ROW_NUMBER() OVER (PARTITION BY Dept ORDER BY Salary DESC) AS rank_in_dept
FROM Employee;

-- RANK: same value = same rank, next rank skips
SELECT Name, Salary,
       RANK() OVER (ORDER BY Salary DESC) AS salary_rank
FROM Employee;
-- If two employees tied at rank 1, next rank is 3 (not 2)

-- DENSE_RANK: same value = same rank, no gaps
SELECT Name, Salary,
       DENSE_RANK() OVER (ORDER BY Salary DESC) AS dense_rank
FROM Employee;
-- If two employees tied at rank 1, next rank is 2

-- NTILE: divide into N equal buckets
SELECT Name, Salary,
       NTILE(4) OVER (ORDER BY Salary) AS quartile
FROM Employee;

-- LAG: access previous row's value
SELECT Name, Salary, Month,
       LAG(Salary, 1) OVER (PARTITION BY EmpID ORDER BY Month) AS prev_month_salary,
       Salary - LAG(Salary, 1) OVER (PARTITION BY EmpID ORDER BY Month) AS change
FROM Monthly_Salary;

-- LEAD: access next row's value
SELECT Name, Month, Salary,
       LEAD(Salary, 1) OVER (PARTITION BY EmpID ORDER BY Month) AS next_month_salary
FROM Monthly_Salary;

-- SUM/AVG as window function (running total)
SELECT Month, Revenue,
       SUM(Revenue) OVER (ORDER BY Month) AS running_total,
       AVG(Revenue) OVER (ORDER BY Month ROWS BETWEEN 2 PRECEDING AND CURRENT ROW) AS moving_avg_3
FROM Sales;
```

---

## 4.10 Stored Procedures and Functions

### Stored Procedure (PostgreSQL)
```sql
CREATE OR REPLACE PROCEDURE enroll_student(
  p_rollno   INT,
  p_courseid VARCHAR(10)
)
LANGUAGE plpgsql
AS $$
BEGIN
  INSERT INTO Enrollment(RollNo, CourseID, EnrollDate)
  VALUES (p_rollno, p_courseid, CURRENT_DATE);
  
  RAISE NOTICE 'Student % enrolled in course %', p_rollno, p_courseid;
EXCEPTION
  WHEN unique_violation THEN
    RAISE EXCEPTION 'Student already enrolled in this course!';
END;
$$;

-- Call the procedure
CALL enroll_student(101, 'CS301');
```

### User-Defined Function
```sql
CREATE OR REPLACE FUNCTION get_dept_avg_salary(p_dept_id INT)
RETURNS DECIMAL
LANGUAGE plpgsql
AS $$
DECLARE
  v_avg DECIMAL;
BEGIN
  SELECT AVG(Salary) INTO v_avg
  FROM Employee
  WHERE DeptID = p_dept_id;
  
  RETURN COALESCE(v_avg, 0);
END;
$$;

-- Use in query
SELECT DeptID, get_dept_avg_salary(DeptID) AS avg_salary
FROM Department;
```

---

## 4.11 Triggers

A **trigger** is code that **automatically executes** when a specified event (INSERT, UPDATE, DELETE) occurs on a table.

```sql
-- Log every salary change
CREATE TABLE Salary_Audit (
  AuditID    SERIAL PRIMARY KEY,
  EmpID      INT,
  OldSalary  DECIMAL,
  NewSalary  DECIMAL,
  ChangedAt  TIMESTAMP DEFAULT NOW(),
  ChangedBy  VARCHAR(50) DEFAULT CURRENT_USER
);

CREATE OR REPLACE FUNCTION log_salary_change()
RETURNS TRIGGER
LANGUAGE plpgsql
AS $$
BEGIN
  IF OLD.Salary != NEW.Salary THEN
    INSERT INTO Salary_Audit(EmpID, OldSalary, NewSalary)
    VALUES (OLD.EmpID, OLD.Salary, NEW.Salary);
  END IF;
  RETURN NEW;
END;
$$;

CREATE TRIGGER salary_change_trigger
AFTER UPDATE OF Salary ON Employee
FOR EACH ROW
EXECUTE FUNCTION log_salary_change();
```

**Trigger Types:**
- `BEFORE INSERT/UPDATE/DELETE` — runs before the operation
- `AFTER INSERT/UPDATE/DELETE` — runs after the operation
- `INSTEAD OF` — replaces the operation (used on views)
- `FOR EACH ROW` — fires once per affected row
- `FOR EACH STATEMENT` — fires once per SQL statement

---

## 4.12 Transactions in SQL

```sql
-- Start transaction
BEGIN;  -- or START TRANSACTION;

UPDATE Account SET Balance = Balance - 1000 WHERE AccID = 'A';
UPDATE Account SET Balance = Balance + 1000 WHERE AccID = 'B';

-- If both succeed:
COMMIT;

-- If anything fails:
ROLLBACK;

-- Partial rollback using SAVEPOINT
BEGIN;
  UPDATE Employee SET Salary = 60000 WHERE EmpID = 101;
  SAVEPOINT after_emp101;
  
  UPDATE Employee SET Salary = 70000 WHERE EmpID = 102;
  -- Oops, made an error for 102:
  ROLLBACK TO after_emp101;
  
  UPDATE Employee SET Salary = 65000 WHERE EmpID = 102;  -- corrected
COMMIT;
```

---

## 4.13 DCL — Data Control Language

```sql
-- Grant privileges
GRANT SELECT, INSERT ON Student TO 'john'@'localhost';
GRANT ALL PRIVILEGES ON DATABASE university TO admin_user;
GRANT SELECT ON Student TO PUBLIC;  -- all users

-- Grant with ability to pass on privileges
GRANT SELECT ON Student TO analyst WITH GRANT OPTION;

-- Revoke privileges
REVOKE INSERT ON Student FROM 'john'@'localhost';
REVOKE ALL PRIVILEGES ON DATABASE university FROM former_admin;
```

---

## 4.14 Common SQL Interview Questions

```sql
-- Q1: Find the 2nd highest salary
SELECT MAX(Salary) FROM Employee
WHERE Salary < (SELECT MAX(Salary) FROM Employee);

-- Using DENSE_RANK (better approach)
SELECT Salary FROM (
  SELECT Salary, DENSE_RANK() OVER (ORDER BY Salary DESC) AS rnk
  FROM Employee
) ranked WHERE rnk = 2;

-- Q2: Find duplicate records
SELECT Name, COUNT(*) FROM Student
GROUP BY Name HAVING COUNT(*) > 1;

-- Q3: Delete duplicates, keep one
DELETE FROM Student
WHERE RollNo NOT IN (
  SELECT MIN(RollNo) FROM Student GROUP BY Name, Email
);

-- Q4: Find employees who earn more than their manager
SELECT e.Name FROM Employee e
JOIN Employee m ON e.ManagerID = m.EmpID
WHERE e.Salary > m.Salary;

-- Q5: Department with maximum employees
SELECT DeptID, COUNT(*) AS cnt FROM Employee
GROUP BY DeptID ORDER BY cnt DESC LIMIT 1;

-- Q6: Running total
SELECT Month, Sales,
       SUM(Sales) OVER (ORDER BY Month) AS running_total
FROM Monthly_Sales;
```

---

## Module 4 — Quick Summary

- DDL: CREATE, ALTER, DROP, TRUNCATE | DML: INSERT, UPDATE, DELETE, SELECT
- Query execution order: FROM→WHERE→GROUP BY→HAVING→SELECT→ORDER BY→LIMIT
- Joins: INNER, LEFT, RIGHT, FULL OUTER, CROSS, SELF
- Subqueries: Simple, Correlated, EXISTS, ANY/ALL
- Window functions: ROW_NUMBER, RANK, DENSE_RANK, LAG, LEAD, running totals
- Views: virtual tables for security and simplicity; Materialized views store data
- Triggers: auto-execute on INSERT/UPDATE/DELETE events
- Transactions: BEGIN, COMMIT, ROLLBACK, SAVEPOINT

---

<a name="module-5"></a>
# Module 5: Database Design Theory & Normalization

---
## 5.1 Functional Dependencies (FD)

A **functional dependency** X → Y means:  
"Knowing the value of X, we can determine the value of Y"

**Notation:** X → Y (X functionally determines Y)

```
RollNo → StudentName   (knowing RollNo, we know exactly one Name)
RollNo → Dept
CourseID → CourseName
(RollNo, CourseID) → Grade  (composite FD — need both to determine Grade)
```

### Properties of FDs (Armstrong's Axioms)

1. **Reflexivity:** If Y ⊆ X, then X → Y  
   (If X contains Y, then X determines Y trivially)

2. **Augmentation:** If X → Y, then XZ → YZ  
   (Adding same attribute to both sides)

3. **Transitivity:** If X → Y and Y → Z, then X → Z

**Derived rules:**
- **Union:** If X → Y and X → Z, then X → YZ
- **Decomposition:** If X → YZ, then X → Y and X → Z
- **Pseudotransitivity:** If X → Y and WY → Z, then WX → Z

### Closure of a Set of Attributes (F+)
The closure of attribute set X (written X⁺) is the **set of all attributes determined by X** given a set of FDs F.

```
Given: R(A, B, C, D, E)
FDs: A→B, B→C, C→D

Find A⁺:
Start: A⁺ = {A}
Apply A→B: A⁺ = {A, B}
Apply B→C: A⁺ = {A, B, C}
Apply C→D: A⁺ = {A, B, C, D}
No more applicable FDs.
A⁺ = {A, B, C, D}

A is NOT a superkey (E is missing from closure)
```

### Canonical Cover (Minimal Cover)
The canonical cover F_c is a **simplified, minimal set of FDs** that is equivalent to F.

Steps to find canonical cover:
1. **Make RHS singleton:** Split FDs with multiple RHS attributes (A→BC becomes A→B, A→C)
2. **Remove extraneous LHS attributes:** Try removing each LHS attribute — if FD still holds, remove it
3. **Remove redundant FDs:** Remove FD if it can be derived from others

---


## 5.2 Normalization in DBMS

Normalization in DBMS is the process of organizing data in a relational database to reduce redundancy, eliminate data anomalies (like insertion, update, and deletion problems), and improve data integrity. It follows a series of rules called **Normal Forms (NF)**.

We usually start with an unnormalized table (or 0NF) and progressively apply the rules to reach higher normal forms. The most commonly used ones in practice are **1NF, 2NF, and 3NF**.

---

## Running Example (Unnormalized Table)

Imagine a university database table that stores student enrollments:

| StudentID | StudentName | CourseID | CourseName        | InstructorName | InstructorOffice |
|-----------|-------------|----------|-------------------|----------------|------------------|
| 101       | John        | C1       | Database          | Dr. Smith      | Room A-101       |
| 101       | John        | C2       | Operating Systems | Dr. Brown      | Room B-202       |
| 102       | Alice       | C1       | Database          | Dr. Smith      | Room A-101       |
| 103       | Bob         | C3       | Computer Networks | Dr. Lee        | Room C-303       |

### Problems here:

- **Redundant data** (e.g., "Dr. Smith" and "Room A-101" repeat for every student taking Database).
- **Insertion anomaly:** Can't add a new instructor without assigning a student/course.
- **Deletion anomaly:** If we delete the only student in a course, we lose instructor info.
- **Update anomaly:** If Dr. Smith moves to a new room, we have to update multiple rows.

### Functional Dependencies:

- `StudentID → StudentName`
- `CourseID → CourseName, InstructorName`
- `InstructorName → InstructorOffice`

> **Primary key (candidate key) = (StudentID + CourseID)** — a composite key.

---

## 1. First Normal Form (1NF)

### Rule:
- Every attribute must have **atomic** (single, indivisible) values.
- No repeating groups or multi-valued attributes.
- Each row must be unique.

Our example table is already in 1NF because all values are atomic (no comma-separated lists like "C1,C2" in one cell).

**If it wasn't in 1NF (hypothetical bad version):**

| StudentID | StudentName | Courses |
|-----------|-------------|---------|
| 101       | John        | C1, C2  |

**How to fix to 1NF:** Split into separate rows (as we already have in the example).

✅ **Our table is now in 1NF.**

---

## 2. Second Normal Form (2NF)

### Rule:
- Must be in 1NF.
- **No partial dependency:** Every non-prime attribute must be fully functionally dependent on the **entire** primary key (not just part of it).

In our table:
- Primary key = `(StudentID, CourseID)`
- Partial dependencies exist:
  - `StudentName` depends only on `StudentID` (not on `CourseID`).
  - `CourseName` and `InstructorName` depend only on `CourseID` (not on `StudentID`).
  - `InstructorOffice` depends on `InstructorName` (which itself depends on `CourseID`).

### How to convert to 2NF:

We split the table into smaller tables so that every non-prime attribute depends on the **whole key**.

**Students** *(StudentID is primary key)*

| StudentID | StudentName |
|-----------|-------------|
| 101       | John        |
| 102       | Alice       |
| 103       | Bob         |

**Courses** *(CourseID is primary key)*

| CourseID | CourseName        | InstructorName |
|----------|-------------------|----------------|
| C1       | Database          | Dr. Smith      |
| C2       | Operating Systems | Dr. Brown      |
| C3       | Computer Networks | Dr. Lee        |

**Enrollments** *(StudentID + CourseID is composite primary key)*

| StudentID | CourseID |
|-----------|----------|
| 101       | C1       |
| 101       | C2       |
| 102       | C1       |
| 103       | C3       |

Now there are no partial dependencies — everything depends on the full primary key of its table.

✅ **Our database is now in 2NF.** Redundancy is reduced, but we still have one issue left…

---

## 3. Third Normal Form (3NF)

### Rule:
- Must be in 2NF.
- **No transitive dependency:** Non-prime attributes must depend **only on the primary key** (not on other non-prime attributes).

In the Courses table above:
- `CourseID → CourseName, InstructorName`
- But `InstructorName → InstructorOffice` *(InstructorOffice depends on InstructorName, which is a non-prime attribute)*

This is a **transitive dependency:** `CourseID → InstructorName → InstructorOffice`.

### How to convert to 3NF:

Split the transitive dependency into its own table.

**Students** *(same as before)*

| StudentID | StudentName |
|-----------|-------------|
| 101       | John        |
| 102       | Alice       |
| 103       | Bob         |

**Instructors** *(InstructorName is primary key)*

| InstructorName | InstructorOffice |
|----------------|------------------|
| Dr. Smith      | Room A-101       |
| Dr. Brown      | Room B-202       |
| Dr. Lee        | Room C-303       |

**Courses** *(now clean)*

| CourseID | CourseName        | InstructorName |
|----------|-------------------|----------------|
| C1       | Database          | Dr. Smith      |
| C2       | Operating Systems | Dr. Brown      |
| C3       | Computer Networks | Dr. Lee        |

**Enrollments** *(same as before)*

Now every non-prime attribute depends directly on the primary key only. No transitive dependencies.

✅ **Our database is now in 3NF.** This is the most common level used in real-world applications.

---

## Boyce-Codd Normal Form (BCNF) — A Stronger Version of 3NF

### Rule:
- Must be in 3NF.
- For every functional dependency `X → Y`, **X must be a super key** (candidate key).

In most cases, 3NF and BCNF are the same. But if there are multiple overlapping candidate keys, BCNF is stricter.

In our example, the tables are already in BCNF because all determinants (left side of `→`) are candidate keys.

> **When BCNF differs:** Suppose a table has two candidate keys and a dependency where one non-key determines part of another key — then we decompose further.

---
---

> ⚠️ **Important:** BCNF decomposition may **not preserve all FDs** (but is lossless-join). 3NF always preserves FDs.

---
## Higher Normal Forms (Quick Overview)

- **4NF:** Eliminates multi-valued dependencies (e.g., one employee has multiple skills and multiple phone numbers independently).
- **5NF (Project-Join Normal Form):** Eliminates join dependencies (very rare in practice).

> You almost never need 4NF or 5NF unless your database has very complex relationships.

---
### Fourth Normal Form (4NF)
A relation is in 4NF if:
- It is in **BCNF**, AND
- It has **no non-trivial multivalued dependencies** (MVD)

> Multivalued Dependency X →→ Y: For each value of X, there is a set of Y values independent of other attributes

**Example of 4NF violation:**
```
Employee_Skills (EmpID, Skill, Language)

An employee can have multiple skills AND multiple languages, independently:
EmpID →→ Skill
EmpID →→ Language
```

**Fix:**
```
Employee_Skills   (EmpID, Skill)
Employee_Languages (EmpID, Language)
```

---

### Fifth Normal Form (5NF) / Project-Join Normal Form (PJNF)
A relation is in 5NF if every **join dependency** is implied by the candidate keys.

Used for rare complex scenarios. Usually not needed in practice.

---
## Summary Table

| Normal Form | Requirement                          | Problem it Solves          | Our Example Status   |
|-------------|--------------------------------------|----------------------------|----------------------|
| 1NF         | Atomic values, no repeating groups   | Multi-valued attributes    | Already satisfied    |
| 2NF         | 1NF + no partial dependency          | Partial key dependency     | After decomposition  |
| 3NF         | 2NF + no transitive dependency       | Transitive dependency      | Final form           |
| BCNF        | 3NF + every determinant is a key     | More complex dependencies  | Also satisfied       |

---

## Benefits of Normalization

- **Less storage** — no duplicate data.
- **Fewer anomalies** — insert/update/delete safely.
- **Easier maintenance.**

> **Trade-off:** Sometimes we *denormalize* (intentionally go back to lower NF) for performance in read-heavy applications (like data warehouses).



## 5.3 Decomposition Properties

When decomposing a relation into smaller ones, two properties must hold:

### 1. Lossless-Join Decomposition
When we JOIN the decomposed tables back, we get the **exact original table** (no spurious tuples, no data loss).

**Test:** For decomposition of R into R1 and R2:
```
R1 ∩ R2 → R1   OR   R1 ∩ R2 → R2
(The common attributes must form a key in at least one of the tables)
```

### 2. Dependency-Preserving Decomposition
All functional dependencies of the original relation can be **checked within individual decomposed tables** (without re-joining).

| Normal Form | Lossless-Join? | Dependency-Preserving? |
|---|---|---|
| 3NF | ✅ Always | ✅ Always |
| BCNF | ✅ Always | ❌ Not always |

---

## 5.4 Step-by-Step Normalization Example

**Given relation:**
```
R (StudentID, StudentName, CourseID, CourseName, InstructorID, InstructorName, InstructorPhone, Grade)

FDs:
StudentID → StudentName
CourseID → CourseName
InstructorID → InstructorName, InstructorPhone
(StudentID, CourseID) → Grade, InstructorID
```

**Step 1: Check 1NF**
All attributes are atomic → ✅ Already in 1NF

**Step 2: Find Primary Key**
(StudentID, CourseID) → determines everything → PK = (StudentID, CourseID)

**Step 3: Check 2NF — Remove partial dependencies**
```
StudentID → StudentName           ← partial dependency!
CourseID → CourseName             ← partial dependency!
```

Decompose:
```
Student (StudentID PK, StudentName)
Course  (CourseID PK, CourseName)
Enrollment (StudentID FK, CourseID FK, InstructorID, Grade)  PK=(StudentID, CourseID)
```

Now check: InstructorID → InstructorName, InstructorPhone in Enrollment
→ InstructorID is non-prime, InstructorName/Phone depend on InstructorID → TRANSITIVE DEPENDENCY!

**Step 4: Check 3NF — Remove transitive dependencies**
```
Instructor (InstructorID PK, InstructorName, InstructorPhone)
Enrollment (StudentID FK, CourseID FK, InstructorID FK, Grade)
```

**Final 3NF Decomposition:**
```
Student    (StudentID PK, StudentName)
Course     (CourseID PK, CourseName)
Instructor (InstructorID PK, InstructorName, InstructorPhone)
Enrollment (StudentID FK, CourseID FK, InstructorID FK, Grade)
```

---

## 5.5 Denormalization

**Denormalization** is the process of intentionally adding redundancy back to a database to **improve read performance**.

**When to denormalize:**
- Read queries are far more frequent than writes
- JOINs across many tables are causing performance bottlenecks
- Analytics/reporting databases (OLAP)

**Techniques:**
- Storing calculated columns (e.g., `total_amount` instead of computing each time)
- Combining tables to avoid JOINs
- Pre-aggregating data

**Trade-off:**
```
Normalized DB   → Less storage, no anomalies, slower reads (more joins)
Denormalized DB → More storage, possible anomalies, faster reads (fewer joins)
```

---

## Module 5 — Quick Summary

- Normalization removes: Insertion, Deletion, and Update Anomalies
- 1NF: Atomic values only
- 2NF: No partial dependencies (full dependency on entire PK)
- 3NF: No transitive dependencies (non-prime → non-prime)
- BCNF: Stricter — every FD's LHS must be a superkey
- 4NF: No multivalued dependencies
- Lossless join: Must always hold; Dependency-preserving: 3NF guarantees, BCNF doesn't
- Canonical cover: minimal equivalent set of FDs

---

<a name="module-6"></a>
# Module 6: Transaction Management & Concurrency Control

---

## 6.1 What is a Transaction?

A **transaction** is a **logical unit of work** that consists of one or more database operations that must all succeed or all fail together.

**Classic Example — Bank Transfer:**
```
Transfer Rs. 1000 from Account A to Account B:

T1: READ(A)          -- read A's balance
T2: A = A - 1000     -- debit A
T3: WRITE(A)         -- write updated A
T4: READ(B)          -- read B's balance
T5: B = B + 1000     -- credit B
T6: WRITE(B)         -- write updated B
```

If the system crashes after T3 but before T6, A is debited but B is never credited → **Inconsistency!** Transactions prevent this.

---

## 6.2 ACID Properties

The four fundamental properties that guarantee database reliability.

### A — Atomicity
**"All or Nothing"**

A transaction either **completes fully** or has **no effect at all**. No partial execution.

```
Debit A AND Credit B → must BOTH succeed
If debit succeeds but credit fails → ROLLBACK everything (as if nothing happened)
```

Implemented by: **Recovery Manager** (using logs)

### C — Consistency
The database must move from one **consistent state to another** consistent state.

```
Before transfer: A=5000, B=3000  → Total = 8000
After transfer:  A=4000, B=4000  → Total = 8000 ✓
```

All integrity constraints must hold after the transaction.

### I — Isolation
**Transactions execute as if they are the only ones running.**

Concurrent transactions should not interfere with each other.

```
T1 is transferring money from A to B.
T2 reads A's balance at the same time.

Without isolation: T2 might see A debited but B not yet credited (dirty read)
With isolation: T2 sees either the before or after state — not the in-between
```

Implemented by: **Concurrency Control** (locks, timestamps)

### D — Durability
Once a transaction is **committed**, its changes are **permanent** — even if the system crashes immediately after.

Implemented by: **Recovery Manager** (write-ahead logging, checkpoints)

---

## 6.3 Transaction States

```
                  ┌─────────────────┐
                  │                 │
             ┌────▼────┐      ┌─────▼─────┐
  BEGIN ──── │  Active  │──────│ Partially │
             └────┬─────┘ fail │ Committed │
                  │            └─────┬─────┘
                  │ fail             │ commit
                  ▼                  ▼
             ┌─────────┐       ┌──────────┐
             │  Failed │──────►│ Committed│
             └────┬─────┘abort └──────────┘
                  │
                  ▼
             ┌──────────┐
             │  Aborted │ (rolled back)
             └──────────┘
```

---

## 6.4 Schedules

A **schedule** is the sequence of operations from multiple concurrent transactions.

**Serial Schedule:** Transactions execute one after another, no overlap.
```
T1: R(A), W(A), R(B), W(B)
T2: R(A), W(A)
— No concurrency, always correct but slow
```

**Concurrent Schedule:** Operations from multiple transactions interleaved.
```
T1: R(A)         W(A)         R(B)     W(B)
T2:      R(A) W(A)       R(B)     W(B)
— May or may not be correct
```

---

## 6.5 Serializability

A concurrent schedule is **serializable** if it produces the same result as some **serial schedule** of the same transactions.

### Conflict Serializability

Two operations **conflict** if:
1. They belong to **different transactions**, AND
2. They access the **same data item**, AND
3. At least one is a **WRITE**

**Conflict pairs:** R-W, W-R, W-W

#### Precedence Graph (Serialization Graph)
Used to test if a schedule is conflict-serializable.

1. Create a node for each transaction
2. Draw an edge Ti → Tj if any operation of Ti **conflicts with** and **comes before** an operation of Tj
3. If the graph has **no cycles → Conflict Serializable**

**Example:**
```
Schedule: R1(A), R2(A), W1(A), R2(B), W2(A), W1(B)

Conflicts:
- W1(A) before W2(A) → T1 → T2
- W1(A) before R2(A)? No, R2(A) comes before W1(A) → T2 → T1

Precedence graph: T1 → T2 and T2 → T1 → CYCLE!
→ NOT conflict serializable
```

### View Serializability

Weaker than conflict serializability. A schedule S is view-equivalent to serial schedule S' if:
1. Initial reads are the same (if Ti reads initial value of X in S, same in S')
2. Updated reads are the same (if Ti reads X written by Tj in S, same in S')
3. Final writes are the same (last write to each item is by the same transaction)

> Every conflict-serializable schedule is view-serializable. The reverse is not always true.

---

## 6.6 Concurrency Control Protocols

### Lock-Based Protocols

**Shared Lock (S / Read Lock):**
- Multiple transactions can hold shared lock on same item simultaneously
- Used for READ operations

**Exclusive Lock (X / Write Lock):**
- Only ONE transaction can hold an exclusive lock
- Blocks both read and write from others
- Used for WRITE operations

**Lock Compatibility:**
```
         S-lock   X-lock
S-lock:  ✅ Yes   ❌ No
X-lock:  ❌ No    ❌ No
```

### Two-Phase Locking (2PL)

The most widely used protocol. Each transaction has two phases:

```
Phase 1 — Growing Phase: Transaction can ACQUIRE locks but NOT release any
Phase 2 — Shrinking Phase: Transaction can RELEASE locks but NOT acquire any
                    
       Locks
        ↑     ╱ Growing
        │    ╱ 
        │   ╱  Lock Point (max locks held)
        │  ╱  ╲
        │ ╱    ╲ Shrinking
        │╱      ╲
        └─────────────────→ Time
```

**2PL guarantees conflict serializability.**

**Variants of 2PL:**

| Variant | Description | Deadlock? |
|---|---|---|
| **Basic 2PL** | Release locks any time in phase 2 | Yes |
| **Strict 2PL** | Hold ALL locks until COMMIT/ROLLBACK | Yes |
| **Conservative (Static) 2PL** | Acquire ALL locks before starting | No (deadlock-free) |
| **Rigorous 2PL** | Hold all X-locks until commit | Yes |

**Strict 2PL** is most common in practice — prevents cascading rollbacks.

---

## 6.7 Deadlock

**Deadlock** occurs when two or more transactions are **waiting for each other** to release locks — creating a circular wait.

```
T1 holds lock on A, waiting for B
T2 holds lock on B, waiting for A
→ Both wait forever = DEADLOCK
```

### Deadlock Detection
Use a **Wait-For Graph (WFG):**
- Node = transaction
- Edge Ti → Tj = Ti is waiting for Tj to release a lock
- If WFG has a **cycle → Deadlock detected**

**Resolution:** Abort one of the transactions in the cycle (the **victim**), usually the one with least cost (fewest updates).

### Deadlock Prevention
**Timestamp-based methods** assign timestamps to transactions:

**Wait-Die (Non-preemptive):**
- Older transaction waits
- Younger transaction dies (aborts and restarts)
```
If Ti (older) requests lock held by Tj (younger): Ti WAITS
If Ti (younger) requests lock held by Tj (older): Ti DIES (aborts)
```

**Wound-Wait (Preemptive):**
- Older transaction wounds (preempts/aborts) younger
- Younger transaction waits
```
If Ti (older) requests lock held by Tj (younger): Tj is WOUNDED (aborted)
If Ti (younger) requests lock held by Tj (older): Ti WAITS
```

Both schemes ensure no circular wait → no deadlock.

### Deadlock Avoidance
**Banker's Algorithm:** Check if granting a lock will lead to a safe state. Complex and rarely used in databases.

---

## 6.8 Timestamp Ordering Protocol

Each transaction Ti is assigned a unique **timestamp TS(Ti)** when it starts.

**Rules:**
- For data item Q with read_TS(Q) and write_TS(Q):

```
If Ti wants to READ Q:
  If TS(Ti) < write_TS(Q) → Ti is late (Q was updated by newer Tx) → ABORT Ti
  Else → Allow read, update read_TS(Q) = max(read_TS(Q), TS(Ti))

If Ti wants to WRITE Q:
  If TS(Ti) < read_TS(Q) → Ti is too late → ABORT Ti
  If TS(Ti) < write_TS(Q) → Ti's write is obsolete → ABORT Ti
  Else → Allow write, update write_TS(Q) = TS(Ti)
```

---

## 6.9 Optimistic Concurrency Control (Validation-Based)

Assumes conflicts are **rare**. Transactions execute freely, validated at commit time.

Three phases:
1. **Read phase:** Read and compute locally (no locks)
2. **Validation phase:** Check for conflicts with committed transactions
3. **Write phase:** If valid → commit; else → abort and restart

Good for **read-heavy** workloads with few conflicts.

---

## 6.10 Multiversion Concurrency Control (MVCC)

Maintains **multiple versions** of a data item. Readers never block writers and writers never block readers.

- Each WRITE creates a new **version** with a timestamp
- Readers access the **appropriate version** based on their timestamp
- Used by: **PostgreSQL, Oracle, MySQL InnoDB**

---

## 6.11 Isolation Levels (SQL Standard)

| Isolation Level | Dirty Read | Non-Repeatable Read | Phantom Read |
|---|---|---|---|
| **READ UNCOMMITTED** | ✅ Possible | ✅ Possible | ✅ Possible |
| **READ COMMITTED** | ❌ Prevented | ✅ Possible | ✅ Possible |
| **REPEATABLE READ** | ❌ Prevented | ❌ Prevented | ✅ Possible |
| **SERIALIZABLE** | ❌ Prevented | ❌ Prevented | ❌ Prevented |

**Definitions:**
- **Dirty Read:** Reading data written by an uncommitted transaction
- **Non-Repeatable Read:** Re-reading data that was modified by another committed transaction
- **Phantom Read:** Re-running a query gets different rows because another transaction inserted/deleted rows

```sql
-- Set isolation level in SQL
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
BEGIN;
  SELECT * FROM Account WHERE owner = 'Aryan';
COMMIT;
```

---

## Module 6 — Quick Summary

- Transaction = atomic unit of work; ACID = Atomicity, Consistency, Isolation, Durability
- Transaction states: Active → Partially Committed → Committed / Failed → Aborted
- Serializability test: Precedence graph — no cycle = conflict serializable
- 2PL: Growing phase (acquire locks) + Shrinking phase (release locks) → guarantees serializability
- Strict 2PL: Hold ALL locks until commit — most commonly used
- Deadlock: circular wait. Detected via Wait-For Graph, handled by aborting victim
- Deadlock Prevention: Wait-Die (old waits, young dies) or Wound-Wait (old wounds young, young waits)
- Isolation levels: READ UNCOMMITTED < READ COMMITTED < REPEATABLE READ < SERIALIZABLE
- MVCC: multiple versions, readers don't block writers (used by PostgreSQL, MySQL)

<a name="module-7"></a>
# Module 7: Database Recovery & Security

---

## 7.1 Why Recovery?

Databases can fail due to:
1. **Transaction failure** — logic error, deadlock, user abort
2. **System failure** — OS crash, power outage (volatile memory lost, disk intact)
3. **Disk failure** — physical disk crash (data lost permanently)
4. **Network failure** — in distributed systems

Recovery brings the database back to a **consistent state** after failure.

---

## 7.2 Storage Types

| Storage | Speed | Persistence | Examples |
|---|---|---|---|
| **Volatile** | Fast | Lost on crash | RAM, Cache |
| **Non-Volatile** | Slow | Survives crash | HDD, SSD |
| **Stable** | — | Never lost (theoretically) | Mirrored disks, RAID |

---

## 7.3 Log-Based Recovery

The **Write-Ahead Log (WAL)** principle: 
> **Log records must be written to stable storage BEFORE the actual data changes.**

Each log record contains:
- `[Transaction_ID, Data_Item, Old_Value, New_Value, LSN (Log Sequence Number)]`

### Types of Log Records:
```
<Ti, start>           — transaction started
<Ti, X, old_val, new_val>  — data X changed from old to new
<Ti, commit>          — transaction committed
<Ti, abort>           — transaction aborted
<checkpoint>          — checkpoint taken
```

### Deferred Update (No-Undo / Redo)
- All changes are held in a **log** until transaction commits
- On commit → write all changes to disk
- On failure → redo committed transactions (no undo needed — data never written before commit)
- REDO operations needed for committed transactions

### Immediate Update (Undo-Redo)
- Changes written to disk **immediately** (before commit)
- On failure:
  - **UNDO** uncommitted transactions (using old values in log)
  - **REDO** committed transactions (ensure durability)

---

## 7.4 Checkpoints

Without checkpoints, recovery must scan the **entire log** from the beginning — very slow!

A **checkpoint** records the state at a point in time. On recovery, we only need to process logs **after the last checkpoint**.

**Checkpoint process:**
1. Write all current log records to stable storage
2. Write all modified buffer blocks to disk
3. Write `<checkpoint>` log record

**Recovery with checkpoints:**
```
After crash:
1. Find last checkpoint in log
2. Redo all committed transactions after checkpoint
3. Undo all active (incomplete) transactions
```

---

## 7.5 ARIES Algorithm (Advanced)

**ARIES (Algorithm for Recovery and Isolation Exploiting Semantics)** is used by most modern DBMSs (IBM DB2, SQL Server).

Three phases:
1. **Analysis:** Scan log from last checkpoint → identify which transactions were active and which pages were dirty at crash
2. **Redo:** Redo ALL operations from the earliest dirty page LSN (even uncommitted — to restore exact crash state)
3. **Undo:** Undo all incomplete (uncommitted) transactions in reverse order

**Key features:**
- Supports partial rollbacks (using CLR — Compensation Log Records)
- Fine-grained locking
- Fuzzy checkpoints (don't stop system during checkpoint)

---

## 7.6 Shadow Paging

An alternative to log-based recovery.

- Maintain two page tables: **current page table** and **shadow page table**
- Modifications go to new pages; shadow page table is never changed
- On commit → shadow becomes current (atomic pointer swap)
- On failure → discard current, revert to shadow

**Advantage:** Simple, no undo/redo  
**Disadvantage:** Fragmentation, no concurrent transactions

---

## 7.7 Database Security

### Authorization
Controls **who can access what** data.

```sql
-- Grant permissions
GRANT SELECT, INSERT ON Student TO analyst;
GRANT SELECT ON Student TO PUBLIC;

-- Revoke permissions
REVOKE INSERT ON Student FROM analyst;

-- Grant with pass-through
GRANT SELECT ON Student TO manager WITH GRANT OPTION;
```

### Role-Based Access Control (RBAC)
Users are assigned **roles**, and roles have permissions.

```sql
-- Create roles
CREATE ROLE student_role;
CREATE ROLE admin_role;

-- Assign permissions to roles
GRANT SELECT ON Grades TO student_role;
GRANT ALL ON Grades TO admin_role;

-- Assign roles to users
GRANT student_role TO 'aryan'@'localhost';
GRANT admin_role TO 'dba'@'localhost';
```

**Advantage:** Easier to manage (change role permissions → all users with that role affected)

### Views for Security
Views can **hide sensitive data** from unauthorized users.

```sql
-- Show only name and dept to general users (hide salary)
CREATE VIEW Public_Employee_Info AS
SELECT EmpID, Name, Dept FROM Employee;

GRANT SELECT ON Public_Employee_Info TO public_user;
-- public_user cannot see Salary column
```

### SQL Injection Prevention

SQL injection is a common attack where malicious SQL is injected through user input.

**Vulnerable code (Python):**
```python
# DANGEROUS - SQL Injection possible
query = "SELECT * FROM User WHERE name='" + user_input + "'"
# If user_input = "' OR '1'='1" → all records returned!
```

**Safe code (parameterized queries):**
```python
# SAFE - Parameterized query
query = "SELECT * FROM User WHERE name = %s"
cursor.execute(query, (user_input,))
```

**Other SQL Injection prevention:**
- Use **prepared statements / parameterized queries** always
- **Validate** all user inputs (whitelist expected values)
- Use an **ORM** (Object-Relational Mapper)
- Apply **least privilege** — DB user has only necessary permissions
- **Stored procedures** instead of dynamic SQL

### Encryption

**Data at Rest:**
- Encrypt database files: AES-256
- Column-level encryption for sensitive data (SSN, credit cards)
- Transparent Data Encryption (TDE) — encrypts entire database file

**Data in Transit:**
- Use **SSL/TLS** for all connections to the database
- Certificate-based authentication

```sql
-- PostgreSQL: require SSL
ALTER USER myuser CONNECTION LIMIT 5;
-- Configure in pg_hba.conf: hostssl all all 0.0.0.0/0 md5
```

### Auditing
Track all database access and changes for compliance and forensics.

```sql
-- PostgreSQL audit logging (pgaudit extension)
ALTER SYSTEM SET pgaudit.log = 'all';

-- Oracle: Fine-Grained Auditing
DBMS_FGA.ADD_POLICY(
  object_schema => 'HR',
  object_name   => 'EMPLOYEES',
  policy_name   => 'audit_salary',
  audit_column  => 'SALARY'
);
```

---

## Module 7 — Quick Summary

- Recovery needed for: transaction failure, system failure, disk failure
- WAL: Write log BEFORE writing actual data
- Deferred update: log all, write on commit (only REDO needed)
- Immediate update: write immediately (UNDO + REDO needed)
- Checkpoints: reduce recovery time by marking safe points
- ARIES: Analysis → Redo → Undo (industry standard)
- Security: GRANT/REVOKE, RBAC, Views for hiding data
- SQL Injection: use parameterized queries, never concatenate user input
- Encryption: AES for data at rest, SSL/TLS for data in transit

---

<a name="module-8"></a>
# Module 8: Storage Structures, Indexing & Query Processing

---

## 8.1 Physical Storage

### File Organization

**Heap (Unordered) File:**
- Records stored in insertion order
- Fast insert, slow search (must scan all)
- Good for: bulk load, full table scans

**Sequential (Sorted) File:**
- Records sorted by a search key
- Fast search (binary search), slow insert
- Good for: range queries on the sorted key

**Hash File:**
- Records stored based on hash(key)
- Very fast equality search, no range queries
- Good for: exact match lookups

### RAID Levels

| RAID | Technique | Benefit | Cost |
|---|---|---|---|
| **RAID 0** | Striping | High performance | No redundancy |
| **RAID 1** | Mirroring | Full redundancy | 2× storage |
| **RAID 5** | Striping + Parity | Good balance | 1 disk overhead |
| **RAID 6** | Striping + 2 Parity | Tolerate 2 disk failures | 2 disk overhead |
| **RAID 10** | RAID 1+0 | High performance + redundancy | 2× storage |

---

## 8.2 Indexing

An **index** is a separate data structure that allows **fast data retrieval** without scanning the entire table.

Analogy: Index at the back of a textbook — you don't read the whole book to find a topic.

### Dense vs. Sparse Index

| Type | Has entry for... | Size | Use case |
|---|---|---|---|
| **Dense** | Every record | Large | Fast equality search |
| **Sparse** | Only some records (one per block) | Small | Sequential scan after finding block |

### Primary vs. Secondary Index

**Primary Index:**
- Built on the **ordering key** (usually PK)
- File is sorted by this key
- One index entry per **data block** (sparse)

**Secondary Index:**
- Built on a **non-ordering attribute**
- File is NOT sorted by this key
- Usually dense (one entry per record)
- May use bucket-level indirection

### Clustered vs. Non-Clustered Index

| Type | Meaning | Count per table |
|---|---|---|
| **Clustered** | Data rows physically sorted in order of index key | Max ONE |
| **Non-Clustered** | Index stores pointers to actual rows; data unsorted | Multiple |

> In most DBMSs, the PRIMARY KEY creates a clustered index by default.

---

## 8.3 B-Tree and B+ Tree (Most Important ⭐)

### B-Tree
- **Balanced** tree where all leaf nodes are at the same depth
- Each node can have multiple keys and children
- Keys AND data pointers stored in internal nodes

**Properties of B-Tree of order m:**
- Every node has at most m children
- Every non-root node has at least ⌈m/2⌉ children
- Root has at least 2 children (unless it's a leaf)
- All leaves at the same level

### B+ Tree (Used by Almost All DBMS)
B+ Tree is an improvement on B-Tree:

- **Data pointers ONLY in leaf nodes** (internal nodes have only keys for routing)
- Leaf nodes are **linked** (like a linked list) → very efficient for range queries
- All keys appear in leaf nodes

```
B+ Tree Structure:

Internal nodes (routing keys only):
         [30 | 60]
        /    |    \
      [10|20] [40|50] [70|80]
      ↕  ↕  ↕  ↕  ↕  ↕  ↕  ↕     ← All leaves linked
     D1 D2 D3 D4 D5 D6 D7 D8      ← Actual data pointers
```

**Why B+ Tree over B-Tree?**
1. Range queries: traverse linked leaf list
2. More keys per internal node (no data pointers) → shallower tree → fewer disk reads
3. All data at same level → uniform access time

---

## 8.4 Hash Indexes

### Static Hashing
- Fixed number of **buckets**
- Hash function: h(key) = key mod N
- **Problem:** Overflow when too many records hash to same bucket; Hard to resize

### Dynamic Hashing (Extendible Hashing)
- Number of buckets grows dynamically
- Uses a **directory** of pointers to buckets
- When bucket overflows → split bucket and double directory

### Linear Hashing
- Buckets split in a **linear, predetermined order** (not necessarily the overflowing bucket)
- No directory needed

---

## 8.5 Bitmap Indexes

Used for **low-cardinality** columns (few distinct values like Gender, Status, Region).

```
Employee (EmpID, Dept)

Dept values: CS, IT, ECE

Bitmap Index:
EmpID | CS  | IT  | ECE
101   | 1   | 0   | 0
102   | 0   | 1   | 0
103   | 0   | 0   | 1
104   | 1   | 0   | 0

Query: WHERE Dept = 'CS' OR Dept = 'IT'
→ Bitwise OR: [1,0,0,1] OR [0,1,0,0] = [1,1,0,1]
→ EmpIDs: 101, 102, 104
```

Very fast for analytics (AND/OR operations on bitmaps), poor for OLTP (frequent updates).

---

## 8.6 Query Processing Pipeline

```
SQL Query
   ↓
1. Parser (check syntax, resolve names)
   ↓
2. Translator (convert SQL to relational algebra expression)
   ↓
3. Query Optimizer (find cheapest execution plan)
   ↓
4. Code Generator (generate executable code)
   ↓
5. Query Executor (execute and return results)
```

---

## 8.7 Query Optimization

The optimizer tries to find the **most efficient execution plan** for a given query.

### Cost-Based Optimization
Estimate cost of different plans using:
- **Table statistics:** Number of rows, distinct values, histograms
- **I/O cost:** Number of disk reads/writes
- **CPU cost:** Computation time

### Heuristic (Rule-Based) Optimization
Apply rules without calculating actual costs:

1. **Push selections down** (filter early → fewer rows to process)
   - σ_c(R ⋈ S) → σ_c(R) ⋈ S (if condition only uses R's attributes)
2. **Push projections down** (reduce columns early → smaller intermediate results)
3. **Perform most selective operations first** (apply most restrictive conditions first)
4. **Use indexes** when available

### Join Strategies

#### Nested-Loop Join (NLJ)
```
For each tuple r in R:
    For each tuple s in S:
        If r.key == s.key: output (r, s)

Cost: |R| × |S| block reads (worst case)
```

#### Block Nested-Loop Join (BNLJ)
```
For each block B_R of R:
    For each block B_S of S:
        For each pair (r in B_R, s in B_S): check join condition

Cost: |R| + |R|/B × |S|  (B = buffer pages)
Better than NLJ when buffer is large
```

#### Sort-Merge Join (SMJ)
1. Sort both R and S on join attribute
2. Merge the sorted relations

```
Cost: Sort_Cost(R) + Sort_Cost(S) + |R| + |S|
Best when both relations are already sorted or index exists
```

#### Hash Join
1. **Build phase:** Hash smaller relation into hash table in memory
2. **Probe phase:** For each tuple in larger relation, probe hash table

```
Cost: 3(|R| + |S|) (if smaller relation fits in memory)
Best for large relations with no existing index
```

| Join Method | Best For | Worst Case |
|---|---|---|
| Nested-Loop | Small tables, indexed inner | Huge tables |
| Block Nested-Loop | No index, limited buffer | — |
| Sort-Merge | Pre-sorted data, equality join | — |
| Hash Join | Large unsorted tables, equality join | — |

---

## 8.8 EXPLAIN / Query Plan Analysis

```sql
-- PostgreSQL: explain query plan
EXPLAIN SELECT * FROM Employee WHERE DeptID = 10;

-- With actual execution stats
EXPLAIN ANALYZE SELECT e.Name, d.DeptName
FROM Employee e JOIN Department d ON e.DeptID = d.DeptID
WHERE d.Location = 'Mumbai';
```

Look for:
- **Seq Scan** → full table scan (consider adding index)
- **Index Scan** → using index (good)
- **Nested Loop / Hash Join / Merge Join** → join algorithm chosen
- **cost=X..Y** → estimated I/O cost

---

## Module 8 — Quick Summary

- File organizations: Heap (fast insert), Sequential (fast range), Hash (fast equality)
- Index types: Dense vs Sparse, Clustered vs Non-clustered, Primary vs Secondary
- B+ Tree: balance tree, data only in leaves, leaves linked → range queries efficient
- Hash index: fast equality, no range queries; Static vs Dynamic (Extendible) hashing
- Bitmap index: low-cardinality columns, analytics workloads
- Query processing: Parse → Translate → Optimize → Execute
- Join algorithms: Nested-Loop, Block NL, Sort-Merge, Hash Join
- Cost-based optimization uses statistics; Heuristic pushes selections/projections down

---

<a name="module-9"></a>
# Module 9: Distributed & Parallel Databases

---

## 9.1 Distributed DBMS (DDBMS)

A **distributed database** stores data across **multiple physical locations** (computers/sites) connected by a network, but appears to users as a single logical database.

**Goals:**
- **Data availability:** If one site fails, others continue
- **Scalability:** Add more sites for more capacity
- **Performance:** Query data at nearest site (low latency)
- **Autonomy:** Each site can manage locally

---

## 9.2 Data Fragmentation

Breaking a table into smaller pieces stored at different sites.

### Horizontal Fragmentation
Split rows based on a condition (like horizontal slicing).

```
Employee Table → 
   Delhi_Employee   (WHERE Location = 'Delhi')
   Mumbai_Employee  (WHERE Location = 'Mumbai')
```

**Correctness conditions:**
- **Completeness:** Every tuple in R appears in at least one fragment
- **Reconstruction:** R = F1 ∪ F2 ∪ ... ∪ Fn (UNION reconstructs original)
- **Disjointness:** No tuple appears in more than one fragment

### Vertical Fragmentation
Split columns (like vertical slicing).

```
Employee(EmpID, Name, Salary, DeptID) →
   F1 (EmpID, Name, DeptID)    — general info
   F2 (EmpID, Salary)          — sensitive info (restricted access)
```

**Reconstruction:** Natural JOIN on primary key

### Hybrid (Mixed) Fragmentation
Combination of horizontal and vertical fragmentation.

---

## 9.3 Data Replication

**Replication** = keeping copies of data at multiple sites.

| Strategy | Description | Pros | Cons |
|---|---|---|---|
| **Full Replication** | Complete DB copy at every site | Max availability | Very high update cost |
| **No Replication** | Each fragment stored once | Low storage | Single point of failure |
| **Partial Replication** | Some fragments replicated | Balance | Moderate complexity |

---

## 9.4 Distributed Query Processing

Query has to be broken into **sub-queries** executed at different sites and results combined.

**Key consideration:** Data must often be **shipped** between sites — network cost is high.

**Optimization:** Minimize data transfer (semi-join strategies, perform selections locally first).

---

## 9.5 Distributed Transaction Management

### Two-Phase Commit (2PC) ⭐
The most important protocol for ensuring **atomicity in distributed transactions**.

**Participants:**
- **Coordinator:** Initiates the commit
- **Participants:** Sites that executed parts of the transaction

**Phase 1 — Prepare Phase:**
```
Coordinator: "Are you ready to commit?" → sends PREPARE to all participants
Participants: 
  → Send READY (YES) if they can commit
  → Send ABORT (NO) if they can't
```

**Phase 2 — Commit Phase:**
```
If ALL participants sent READY:
  Coordinator → sends COMMIT to all
  Participants → commit, send ACK

If ANY participant sent ABORT:
  Coordinator → sends ABORT to all
  Participants → rollback
```

**Problem with 2PC:**
- **Blocking:** If coordinator crashes in phase 2, participants are stuck (they voted YES but don't know final decision)

### Three-Phase Commit (3PC)
Adds a **pre-commit phase** to reduce the blocking problem of 2PC.

Phases: Prepare → Pre-commit → Commit

**Still not perfect** — can fail in network partition scenarios (but reduces blocking significantly).

---

## 9.6 Concurrency Control in Distributed Systems

**Extended 2PL:** Apply locking at each site; a global deadlock can span multiple sites.

**Global Deadlock Detection:**
Each site builds a local Wait-For Graph. A central site collects all local WFGs and combines them to detect global cycles.

**Distributed Timestamp Ordering:**
Timestamps assigned using synchronized clocks (e.g., Lamport timestamps).

---

## 9.7 Parallel Databases

Use **multiple processors** to execute queries faster (parallelism within one database system).

### Shared-Memory Architecture
All processors share one large memory and disk.
- **Pros:** Easy to program, fast communication
- **Cons:** Limited scalability (memory bus bottleneck), expensive

### Shared-Disk Architecture
All processors share disks but have their own memory.
- **Pros:** Scales better than shared-memory
- **Cons:** Disk contention, cache coherency issues

### Shared-Nothing Architecture (Most Scalable ⭐)
Each processor has its own memory AND disk. Communicate via network.
- **Pros:** Scales massively (used by Hadoop, Google Spanner)
- **Cons:** Complex programming, network overhead

### Types of Parallelism

**Inter-query parallelism:** Multiple queries run simultaneously on different processors.

**Intra-query parallelism:** A single query is split and executed in parallel:
- **Intra-operation:** One operation (e.g., scan) done in parallel
- **Inter-operation:** Different operations in a query pipeline run simultaneously

---

## Module 9 — Quick Summary

- DDBMS stores data across multiple sites; appears as one logical DB
- Fragmentation: Horizontal (rows) → UNION to reconstruct; Vertical (columns) → JOIN to reconstruct
- Replication: Full, None, or Partial — trade-off between availability and update cost
- 2PC: Prepare phase + Commit phase — ensures distributed atomicity
- 2PC is blocking; 3PC reduces blocking
- Shared-Nothing architecture: most scalable (used by Hadoop, modern cloud DBs)

---

<a name="module-10"></a>
# Module 10: NoSQL, NewSQL & Modern Database Paradigms

---

## 10.1 Why NoSQL?

Relational databases struggle with:
- **Huge scale** (billions of users, petabytes of data)
- **Flexible/unstructured** data (no fixed schema)
- **High write throughput** (social media, IoT, logs)
- **Distributed deployments** across many cheap servers

NoSQL = "**Not Only SQL**" — not a replacement, but an alternative for specific use cases.

---

## 10.2 CAP Theorem ⭐

**Theorem:** A distributed system can guarantee at most **2 of the 3** properties:

```
         Consistency
        /
       /
      /______ 
     /        \
Availability   Partition Tolerance
```

| Property | Meaning |
|---|---|
| **Consistency (C)** | All nodes see the same data at the same time (like linearizability) |
| **Availability (A)** | Every request gets a response (no timeout/error) |
| **Partition Tolerance (P)** | System works even if network splits some nodes |

**In reality:** Network partitions WILL happen, so we must choose between C and A:
- **CP systems** (prefer consistency): MongoDB, HBase, Zookeeper
- **AP systems** (prefer availability): Cassandra, CouchDB, DynamoDB
- **CA systems** (only in single-node setups): Traditional RDBMS (MySQL, PostgreSQL)

---

## 10.3 BASE vs. ACID

| ACID | BASE |
|---|---|
| **A**tomicity | **B**asically **A**vailable |
| **C**onsistency | **S**oft state |
| **I**solation | **E**ventually consistent |
| **D**urability | — |

**Eventually Consistent:** After some time (without new updates), all replicas will converge to the same value.

---

## 10.4 NoSQL Database Types

### 1. Key-Value Stores — Redis

Simplest model: each item stored as a **key → value** pair.

```
key: "user:101"
value: {"name": "Aryan", "age": 20, "city": "Delhi"}
```

**Redis examples:**
```bash
SET user:101 '{"name":"Aryan","age":20}'
GET user:101

# With expiry (TTL)
SET session:xyz "token123" EX 3600   # expires in 1 hour

# Increment counter
INCR page_views:homepage

# Lists
LPUSH notifications:user101 "New message"
LRANGE notifications:user101 0 9

# Sets
SADD user:101:friends "102" "103" "104"
SMEMBERS user:101:friends
```

**Use cases:** Session management, caching, leaderboards, pub/sub messaging, rate limiting

### 2. Document Stores — MongoDB

Data stored as **JSON-like documents** (BSON in MongoDB). Flexible schema.

```json
// Student document
{
  "_id": ObjectId("507f1f77bcf86cd799439011"),
  "rollNo": 101,
  "name": "Aryan Kumar",
  "dept": "CS",
  "courses": ["DBMS", "OS", "CN"],
  "address": {
    "city": "Delhi",
    "state": "Delhi",
    "pin": "110001"
  },
  "grades": [
    {"course": "DBMS", "score": 92},
    {"course": "OS", "score": 85}
  ]
}
```

**MongoDB Operations:**
```javascript
// Insert
db.students.insertOne({name: "Aryan", dept: "CS", age: 20})
db.students.insertMany([{name: "Priya"}, {name: "Rahul"}])

// Query
db.students.find({dept: "CS"})
db.students.find({age: {$gt: 18}})
db.students.find({name: /^A/})  // regex

// Update
db.students.updateOne({rollNo: 101}, {$set: {age: 21}})
db.students.updateMany({dept: "CS"}, {$inc: {gpa: 0.1}})

// Delete
db.students.deleteOne({rollNo: 101})

// Aggregation Pipeline
db.students.aggregate([
  {$match: {dept: "CS"}},                // filter
  {$group: {_id: "$dept", avgAge: {$avg: "$age"}}},  // group
  {$sort: {avgAge: -1}}                  // sort
])
```

**Use cases:** Content management, catalogs, user profiles, real-time analytics

### 3. Column-Family Stores — Cassandra

Data stored in **columns grouped into column families**. Optimized for write-heavy workloads.

```cql
-- Create table (CQL — Cassandra Query Language)
CREATE TABLE students (
  student_id UUID PRIMARY KEY,
  name TEXT,
  dept TEXT,
  age INT
);

-- Insert
INSERT INTO students (student_id, name, dept)
VALUES (uuid(), 'Aryan', 'CS');

-- Query (must use partition key)
SELECT * FROM students WHERE student_id = some_uuid;
```

**Cassandra's model:**
- Data distributed across nodes by **partition key**
- Optimized for writes (append-only log structure — LSM-tree)
- **No joins** — denormalize data instead
- Eventually consistent (tunable consistency)

**Use cases:** IoT sensor data, time-series, write-heavy applications (Netflix, Instagram)

### 4. Graph Databases — Neo4j

Data stored as **nodes, edges (relationships), and properties**.

**Perfect for:** Social networks, recommendation engines, fraud detection, knowledge graphs

```cypher
// Create nodes
CREATE (aryan:Person {name: 'Aryan', age: 20})
CREATE (priya:Person {name: 'Priya', age: 21})
CREATE (dbms:Course {name: 'DBMS'})

// Create relationships
MATCH (a:Person {name: 'Aryan'}), (b:Person {name: 'Priya'})
CREATE (a)-[:FRIENDS_WITH]->(b)

MATCH (a:Person {name: 'Aryan'}), (c:Course {name: 'DBMS'})
CREATE (a)-[:ENROLLED_IN]->(c)

// Queries
// Find all friends of Aryan
MATCH (a:Person {name: 'Aryan'})-[:FRIENDS_WITH]->(friends)
RETURN friends.name

// Find shortest path
MATCH path = shortestPath(
  (a:Person {name: 'Aryan'})-[*]-(b:Person {name: 'Priya'})
)
RETURN path

// Recommend courses (friends' courses not taken by Aryan)
MATCH (a:Person {name: 'Aryan'})-[:FRIENDS_WITH]->(friend)
      -[:ENROLLED_IN]->(course)
WHERE NOT (a)-[:ENROLLED_IN]->(course)
RETURN course.name, COUNT(*) AS friend_count
ORDER BY friend_count DESC
```

---

## 10.5 NewSQL Databases

NewSQL databases provide **ACID guarantees + SQL** with **horizontal scalability** of NoSQL.

| Database | Key Feature |
|---|---|
| **Google Spanner** | Globally distributed, TrueTime API for global consistency |
| **CockroachDB** | PostgreSQL-compatible, survives datacenter failures |
| **VoltDB** | In-memory, high throughput OLTP |
| **TiDB** | MySQL-compatible, HTAP (hybrid OLTP + OLAP) |

---

## 10.6 Data Warehousing & OLAP

### OLTP vs. OLAP

| Feature | OLTP | OLAP |
|---|---|---|
| **Purpose** | Day-to-day operations | Analytics, reporting |
| **Query type** | Simple, small | Complex, large aggregations |
| **Data** | Current | Historical |
| **Updates** | Frequent INSERT/UPDATE/DELETE | Mostly read-only |
| **DB design** | Normalized | Denormalized (Star/Snowflake) |
| **Examples** | Banking, e-commerce | Data warehouse, BI tools |

### Star Schema
Central **fact table** surrounded by **dimension tables** (like a star).

```
             Time_Dim
                |
Customer_Dim —[Sales_Fact]— Product_Dim
                |
            Region_Dim

Sales_Fact (TimeID FK, CustomerID FK, ProductID FK, RegionID FK, Amount, Quantity)
```

### Snowflake Schema
Like star schema but dimension tables are **normalized** (further broken down).

```
Category_Dim ← Product_Dim ←
                              [Sales_Fact]
City_Dim ← Region_Dim ←
```

### OLAP Operations
- **Roll-up (Drill-up):** Aggregate data at higher level (monthly → quarterly → yearly)
- **Drill-down:** Move to lower granularity (yearly → monthly → daily)
- **Slice:** Select one dimension (only 2023 data)
- **Dice:** Select multiple dimensions (2023 data for CS dept in Delhi)
- **Pivot:** Rotate the data cube (rows become columns)

### ETL (Extract, Transform, Load)
Process to move data from operational systems to data warehouse.

```
Source Systems (OLTP DBs)
       ↓
   EXTRACT (pull raw data)
       ↓
  TRANSFORM (clean, aggregate, conform)
       ↓
     LOAD (into Data Warehouse)
       ↓
  Data Warehouse (for analytics)
```

---

## 10.7 Choosing the Right Database

| Use Case | Best Choice |
|---|---|
| Complex transactions, strong consistency | **PostgreSQL, MySQL (RDBMS)** |
| Caching, sessions, real-time counters | **Redis (Key-Value)** |
| Flexible schema, documents, catalogs | **MongoDB (Document)** |
| Time-series, IoT, high write throughput | **Cassandra, InfluxDB** |
| Social graphs, recommendations, fraud | **Neo4j (Graph)** |
| Analytics, reporting on big data | **Snowflake, BigQuery, Redshift** |
| Global scale + ACID | **Google Spanner, CockroachDB** |

---

## Module 10 — Quick Summary

- NoSQL: for scale, flexibility, distributed systems
- CAP Theorem: only 2 of Consistency, Availability, Partition Tolerance
- BASE: Basically Available, Soft state, Eventually consistent
- Key-Value (Redis): caching, sessions; Document (MongoDB): flexible schemas
- Column-Family (Cassandra): write-heavy, IoT; Graph (Neo4j): relationships
- NewSQL: horizontal scalability + ACID (Spanner, CockroachDB)
- Star Schema: fact + dimensions; OLAP: Roll-up, Drill-down, Slice, Dice
- ETL: Extract from source, Transform, Load into warehouse

---

<a name="module-11"></a>
# Module 11: Emerging Trends & Advanced Topics

---

## 11.1 Cloud Databases

Cloud databases are managed database services — no hardware to maintain.

| Service | Provider | Type |
|---|---|---|
| **RDS** | AWS | Managed RDBMS (MySQL, PostgreSQL, etc.) |
| **Aurora** | AWS | MySQL/PostgreSQL-compatible, 5× faster |
| **DynamoDB** | AWS | Serverless, Key-Value/Document |
| **Cosmos DB** | Azure | Multi-model (Key-Value, Document, Graph) |
| **Cloud Spanner** | Google | Globally distributed NewSQL |
| **BigQuery** | Google | Serverless analytics/OLAP |
| **Firestore** | Google | Serverless document store |

**Benefits of Cloud DBs:**
- **Managed:** Automatic backups, patching, scaling
- **Elastic:** Scale up/down instantly based on load
- **Global:** Multi-region replication built-in
- **Pay-per-use:** No upfront hardware cost

---

## 11.2 Big Data Integration

### Hadoop Ecosystem
```
HDFS (Storage) + MapReduce (Processing)
       +
Hive (SQL on Hadoop) + HBase (Column store on HDFS)
       +
YARN (Resource management)
```

**Hive SQL example:**
```sql
-- SQL-like queries on Hadoop
SELECT dept, COUNT(*), AVG(salary)
FROM employees
GROUP BY dept
HAVING COUNT(*) > 100;
```

### Apache Spark
In-memory big data processing (100× faster than Hadoop MapReduce).

**Spark SQL:**
```python
from pyspark.sql import SparkSession

spark = SparkSession.builder.appName("DBMS").getOrCreate()

# Read data
df = spark.read.csv("students.csv", header=True)

# SQL query
df.createOrReplaceTempView("students")
result = spark.sql("SELECT dept, AVG(age) FROM students GROUP BY dept")
result.show()
```

---

## 11.3 Database Tuning & Performance

### Query Hints
Force the optimizer to use a specific index or join method:

```sql
-- PostgreSQL: disable sequential scan (force index use)
SET enable_seqscan = OFF;

-- MySQL: Use specific index
SELECT * FROM Employee USE INDEX (idx_dept) WHERE DeptID = 10;

-- Oracle: hints
SELECT /*+ INDEX(e idx_dept) */ * FROM Employee e WHERE DeptID = 10;
```

### Statistics and Autovacuum
```sql
-- Update statistics (PostgreSQL)
ANALYZE Employee;

-- Vacuum reclaims dead rows
VACUUM ANALYZE Employee;
```

### Connection Pooling
Reuse database connections instead of creating new ones for each request.
- Tools: **PgBouncer** (PostgreSQL), **ProxySQL** (MySQL)

### Partitioning
Split large tables into smaller **partitions** for better performance.

```sql
-- Range Partitioning (PostgreSQL)
CREATE TABLE sales (
  sale_id   INT,
  sale_date DATE,
  amount    DECIMAL
) PARTITION BY RANGE (sale_date);

CREATE TABLE sales_2023 PARTITION OF sales
    FOR VALUES FROM ('2023-01-01') TO ('2024-01-01');
CREATE TABLE sales_2024 PARTITION OF sales
    FOR VALUES FROM ('2024-01-01') TO ('2025-01-01');
```

### AI/ML in DBMS (Autonomous Databases)
- **Query auto-tuning:** AI suggests indexes based on query patterns
- **Anomaly detection:** Unusual queries flagged automatically
- **Oracle Autonomous DB:** Self-driving, self-securing, self-repairing
- **Amazon Aurora ML:** Run ML predictions directly in SQL

---

## 11.4 Time-Series Databases

Optimized for **time-stamped data** (metrics, IoT, monitoring).

**InfluxDB:**
```sql
-- Write data
INSERT cpu_usage,host=server01 value=72.5 1617981600000000000

-- Query (InfluxQL)
SELECT mean(value) FROM cpu_usage
WHERE time >= now() - 1h
GROUP BY time(5m), host
```

**Other time-series DBs:** TimescaleDB (PostgreSQL extension), Prometheus, QuestDB

**Use cases:** Server monitoring, IoT sensors, stock prices, weather data

---

## 11.5 Vector Databases (AI Era ⭐)

Vector databases store and search **high-dimensional vectors** (embeddings from ML models).

Used for:
- **Semantic search** (search by meaning, not keywords)
- **Recommendation systems**
- **Image similarity search**
- **RAG (Retrieval-Augmented Generation)** for LLM applications

**Popular options:** Pinecone, Weaviate, Qdrant, pgvector (PostgreSQL extension)

```python
# Using pgvector (PostgreSQL)
# Store text embeddings and find similar documents
CREATE EXTENSION vector;

CREATE TABLE documents (
  id    SERIAL PRIMARY KEY,
  text  TEXT,
  embedding VECTOR(1536)  -- OpenAI embedding dimension
);

-- Find 5 most similar documents (cosine similarity)
SELECT text, 1 - (embedding <=> query_embedding) AS similarity
FROM documents
ORDER BY embedding <=> query_embedding
LIMIT 5;
```

---

## 11.6 Graph Databases for AI/Knowledge Graphs

Knowledge graphs represent relationships between concepts:
- Google Knowledge Graph (powers "knowledge panels")
- Facebook Social Graph
- LinkedIn Professional Graph

RDF (Resource Description Framework) and SPARQL for semantic web data.

---

## 11.7 Blockchain Databases

**Blockchain** = distributed, immutable, append-only ledger.

| Feature | Traditional DB | Blockchain DB |
|---|---|---|
| Mutable | Yes | No (append-only) |
| Trusted authority | Centralized admin | Decentralized consensus |
| Speed | Fast | Slow |
| Transparency | Private | Transparent (public blockchains) |
| Use case | General | Transactions, supply chain, smart contracts |

**Examples:** Hyperledger Fabric (enterprise), Amazon QLDB (quantum ledger DB)

---

## 11.8 Database Security & Privacy (GDPR Era)

### GDPR Compliance Requirements
- **Right to be forgotten:** Must be able to delete all data about a person
- **Data minimization:** Collect only necessary data
- **Consent management:** Track when and what data was consented to
- **Data breach notification:** Notify within 72 hours

**Implementation:**
```sql
-- Right to be forgotten
DELETE FROM UserProfiles WHERE user_id = 'EU_USER_12345';
DELETE FROM OrderHistory WHERE user_id = 'EU_USER_12345';
-- Must cascade to all tables with user data
```

### Differential Privacy
Adds **mathematical noise** to query results to protect individual privacy while preserving aggregate statistics.

```
Real query result: 145 patients have condition X
With differential privacy: Result reported as 143 or 147 (random noise added)
→ Individual privacy protected, statistical insight preserved
```

Used by: Apple (iOS analytics), Google (Chrome usage stats), US Census Bureau

---

## 11.9 Future Trends

### Autonomous Databases
Self-managing databases that tune themselves:
- Automatic index creation/removal
- Self-healing after failures
- Automatic scaling
- **Oracle Autonomous Database** is the current leader

### In-Memory Databases
Store ALL data in RAM for ultra-low latency:
- **Redis** (most popular), **VoltDB**, **H2**, **SAP HANA**
- 1000× faster than disk-based DBs
- RAM prices dropping, making this more feasible

### Multi-Model Databases
Single database handles multiple data models:
- **ArangoDB:** Document + Graph + Key-Value
- **Azure Cosmos DB:** Key-Value + Document + Graph + Column
- Reduces operational complexity

### Quantum-Safe Encryption
Current encryption (RSA, ECC) will be breakable by quantum computers.
- NIST standardizing **post-quantum cryptography** algorithms
- Databases will need to migrate to quantum-safe algorithms (CRYSTALS-Kyber, CRYSTALS-Dilithium)

---

## Module 11 — Quick Summary

- Cloud DBs: RDS, Aurora, DynamoDB, Cosmos DB, BigQuery — managed, elastic, pay-per-use
- Big Data: Hadoop (batch), Spark (in-memory, fast), Hive (SQL on Hadoop)
- Time-series DBs: InfluxDB, TimescaleDB — for metrics, IoT, monitoring
- Vector DBs: Pinecone, pgvector — for AI/ML embeddings and semantic search
- Blockchain DBs: Immutable, decentralized ledger
- GDPR: right to be forgotten, data minimization, consent
- Differential privacy: add noise to protect individuals, preserve aggregates
- Future: Autonomous DBs, In-memory, Multi-model, Quantum-safe encryption

---

<a name="cheat-sheet"></a>
# Quick Revision Cheat Sheet

---

## 🔑 Most Important Concepts for Exams & Interviews

---

### Normal Forms — Quick Reference
```
1NF → Atomic values, no repeating groups
2NF → 1NF + No partial dependencies (non-key attr depends on WHOLE PK)
3NF → 2NF + No transitive dependencies (non-key → non-key)
BCNF → Every FD's LHS is a superkey (stricter than 3NF)
4NF → BCNF + No multivalued dependencies
```

### Keys — Quick Reference
```
Super Key      → Any set of attrs that uniquely identifies tuples
Candidate Key  → Minimal super key (irreducible)
Primary Key    → Chosen candidate key (unique + NOT NULL)
Foreign Key    → References PK of another table
Composite Key  → PK made of 2+ attributes
Surrogate Key  → Artificial auto-increment key
```

### ACID Properties
```
Atomicity    → All or Nothing
Consistency  → DB moves from one valid state to another
Isolation    → Transactions don't interfere
Durability   → Committed data survives failures
```

### SQL Execution Order
```
FROM → JOIN → WHERE → GROUP BY → HAVING → SELECT → DISTINCT → ORDER BY → LIMIT
```

### Relational Algebra Operators
```
σ   → Selection (filter rows)
π   → Projection (filter columns)
∪   → Union
∩   → Intersection
−   → Set difference
×   → Cartesian product
⋈   → Natural join
ρ   → Renaming
÷   → Division
```

### Concurrency Control
```
2PL:  Growing phase (acquire) → Shrinking phase (release) → Serializability
Strict 2PL: Hold ALL locks until commit
MVCC: Multiple versions → readers never block writers (PostgreSQL uses this)
```

### CAP Theorem
```
C = Consistency (all see same data)
A = Availability (always responds)
P = Partition tolerance (works despite network splits)
→ Can have at most 2 of 3
```

### NoSQL Types
```
Key-Value    → Redis (cache, sessions)
Document     → MongoDB (flexible schemas)
Column-Family → Cassandra (high-write throughput, IoT)
Graph        → Neo4j (social networks, recommendations)
```

### Recovery
```
WAL: Write log BEFORE writing data
ARIES: Analysis → Redo → Undo
2PC: Prepare (vote) → Commit/Abort (decide) → for distributed tx
```

---

## 📝 Frequently Asked Interview Questions

**Q1: What is the difference between DELETE, TRUNCATE, and DROP?**
- DELETE: removes rows conditionally, can rollback, triggers fire
- TRUNCATE: removes all rows, cannot rollback (DDL), resets auto-increment
- DROP: removes entire table structure and data

**Q2: What is the difference between HAVING and WHERE?**
- WHERE filters individual rows (before grouping, no aggregates allowed)
- HAVING filters groups (after GROUP BY, can use aggregates)

**Q3: What is a deadlock and how to prevent it?**
- Circular wait between transactions for locks
- Prevention: Wait-Die, Wound-Wait, acquire all locks before starting

**Q4: What is BCNF and how does it differ from 3NF?**
- BCNF: Every FD's LHS is a superkey (stricter)
- 3NF allows LHS to not be superkey IF RHS is a prime attribute
- BCNF may lose dependency preservation; 3NF always preserves

**Q5: Explain the difference between a clustered and non-clustered index.**
- Clustered: data rows physically ordered by index key; only one per table
- Non-clustered: separate structure with pointers; multiple per table

**Q6: What is a correlated subquery?**
- Subquery that references columns from the outer query
- Executed once per row of the outer query (can be slow)

**Q7: Explain MVCC.**
- Multiple versions of data stored
- Readers access old versions, writers create new versions
- No read-write conflicts → high concurrency
- Used by PostgreSQL, Oracle, MySQL InnoDB

**Q8: What is the difference between 2PC and ARIES?**
- 2PC: distributed commit protocol for atomicity across multiple sites
- ARIES: single-site recovery algorithm (Analysis-Redo-Undo)

**Q9: When would you choose NoSQL over SQL?**
- Unstructured/flexible schema data
- Massive horizontal scalability needed
- High write throughput (IoT, logs)
- Specific data models (graph, time-series)

**Q10: What is a View? Can you always update through a view?**
- Virtual table based on a SELECT query
- Updatable only if: single base table, no DISTINCT/GROUP BY/HAVING, no aggregates, no set operations

---

## 📊 Important Formulas and Theorems

### B+ Tree Height
```
Height h = ⌈log_⌈n/2⌉(K)⌉  where n = order, K = number of keys
Search cost = h disk reads
```

### Conflict Serializability
```
Test: Build precedence graph → No cycle = Conflict Serializable
```

### 2PC Phases
```
Phase 1: Coordinator → PREPARE → Participants vote (READY/ABORT)
Phase 2: Coordinator → COMMIT (if all READY) or ABORT (if any ABORT)
```

### Lossless Join Test
```
R decomposed into R1 and R2 is lossless if:
(R1 ∩ R2) → R1  OR  (R1 ∩ R2) → R2
```

### Armstrong's Axioms
```
1. Reflexivity: Y ⊆ X → X → Y
2. Augmentation: X → Y → XZ → YZ
3. Transitivity: X → Y, Y → Z → X → Z
```

---

## 🎯 Topic-wise Exam Weightage

| Topic | Exam Weight | Interview Weight |
|---|---|---|
| SQL (all types of queries) | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| Normalization | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ |
| ACID & Transactions | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| ER Model & Mapping | ⭐⭐⭐⭐ | ⭐⭐⭐ |
| Concurrency Control | ⭐⭐⭐⭐ | ⭐⭐⭐ |
| Indexing & B+ Trees | ⭐⭐⭐ | ⭐⭐⭐⭐ |
| Relational Algebra | ⭐⭐⭐ | ⭐⭐ |
| Recovery | ⭐⭐⭐ | ⭐⭐⭐ |
| NoSQL | ⭐⭐ | ⭐⭐⭐⭐ |
| Distributed DB | ⭐⭐ | ⭐⭐ |

---

*These notes cover the complete DBMS syllabus from fundamentals to advanced topics. Review each module before exams and focus heavily on SQL and Normalization for maximum marks.*
