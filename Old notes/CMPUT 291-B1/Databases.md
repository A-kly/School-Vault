# What is a database?
- Very big integrated collection of data
- Models real world enterprises info
- uses [[Querying relations|queries]]

- ### [[The Entity-Relationship Model]] (important):
	- Entities (students, courses)
	- relationships (student 12345  __is taking__ c291)
- What is a database management system? (DBMS)
	- software designed to manage database 
	- makes life easier
- Non database approach
	- One data set per program
	- programmer defines and implements storage structures, accessing methods, etc.
- issues:
	- many files with different structures
	- redundant storage (sometimes)
	- inconsistent copies
	- expensive updates
	- incorrect data
	- data exchange issues btw applications

- Databases are _Atomic_ like CSRIs

- ### Basic idea, Why to use?:
	- remove details related to data storage and access from application programs
	- Move all workings into DBMS
	- less redundancy
	- less risk of inconsistency
	- less dev time
	- uniform data administration
	- Concurrent accesses, recovery from crashes
	- **And most importantly, data independence** 

- ### Three Schema Levels:
- Schema: description of data structures and other aspects
- External Schema (HIGH):
	- What application programs and users "see"
- Conceptual schema (MID):
	- description of the logical structure of data
- Physical Schema (LOW):
	- file structures and indexes being used, physical/file structure

- Data independence:
	- Application programs are unaffected by changes in storage structure
	- Logical Data Independent:
		- Implementaion of logical structure can change
	- Physical data independence:
		- Implementation of structure can change

### DBMS Functionality:
- data definition
- data manipulation
    - database recovery (atomic accesses, etc)
    - query optimization

### Data Model: 

- We need a model for describing:
	- The structure of data and constraints
	- Operations on data
- The model describes data at some abstraction layer (schema)
	- External
	- Conceptual
	- Physical

### Relational Databases

- Basic idea:
	- Organize data in a set of tables
	- view each table as a set of rows
	- uses [[Querying relations]]
- Definition
	- A _relational database_ is a set of relations (tables)
	- A _relation_ consists of 
		- Instance: Table content, rows and columns
		- Schema: Table structure, name and type of columns
	- for formally, a relation is a set of rows (tuples)
	- *Cardinality*: number of rows
	- *Degree*: number of columns
		- Exclude title
	- *Domain*: set of values from which the values of an attribute are drawn
		- eg: CHARACHTER is limited to 32 bits (int)



### Integrity Constraints (ICs)  
-  Conditions that hold for _any_ instance of the database,  
	- e.g., _domain constraints_, [[Keys & Key Constraints|key]] constraints
	- defined when schema is defined.  
	- checked when relations are modified.  
- A _legal_ instance of a relation is one that satisfies all specified ICs.  
	- DBMS does not allow illegal instances.  
- As the DBMS checks ICs, stored data is more faithful to real-world meaning.

![[Keys & Key Constraints#Foreign Keys, Referential Integrity]]

### Enforcing referential Integrity
- What if an Enrolled tuple with not existent SID is inserted?
	- reject it!
- What if a tuple in Students is deleted?
	- Delete all enrolled tuples that refer to it OR
	- dissallow deletion of student OR
	- Set sid in Enrolled tuples that refer to it to a default sid. (NULL)

### Referential Integrity in SQL/92

- SQL/92 (and SQL/99) supports all options on deletes and updates.
	- Default is NO ACTION (delete/update is rejected)  
	- CASCADE (also delete/update all tuples that refer to deleted/updated tuple)  
	- SET NULL / SET DEFAULT (sets foreign key value of referencing tuple)

>[!example]
```sql
CREATE TABLE Enrolled  
(sid CHAR(8),  
cid CHAR(8),  
grade CHAR(2),  
PRIMARY KEY (sid,cid),  
FOREIGN KEY (sid)  
REFERENCES Students  
ON DELETE NO ACTION  
ON UPDATE CASCADE );
```

### Where do Integrity Constraints (ICs) Come From?

- real world data semantics
	- IC is statement about all possible instances
	- We cannot infer that an IC is true by looking at an instance.
	- From example, we know name is not a key, but the assertion that sid is a key is given to us.
- “Primary key / foreign key” ICs are the most common; more general ICs supported too.

![[Pasted image 20230110120301.png]]


### External Level
- Applications can access data through some views  
	- Different views of data for different categories of users  
	- A view is computed (from data in the conceptual level)
- Mapping from external to conceptual schema is done by DBMS.  
- Conceptual schema can be changed without changing applications:  
	- Logical data independence.

### Views
- A view is just a relation, but we store a definition, rather than a set of tuples.
```sql
CREATE VIEW YoungActiveStudents (name)  
AS SELECT S.name  
FROM Students S, Enrolled E  
WHERE S.sid = E.sid and S.age<21;
```
- Views can be dropped using the DROP VIEW command.
- Views can be used to present necessary information (or a summary), while hiding details in underlying relation(s).  
- Given YoungActiveStudents, but not Students or Enrolled, we can find young students who are enrolled, but not the cid’s of or grade’s in the courses they are enrolled in.