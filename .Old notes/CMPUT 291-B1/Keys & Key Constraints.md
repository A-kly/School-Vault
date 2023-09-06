										
### Primary key constraints
- A set of fields is a _key_ for a relation if it is both:
	1. Unique: No two distinct tuples can be the same in all key fields
	2. minimal: no subset of a key is a key
- a relation can have more than one key:
	- _Candidate Key_: any key of the relation
	- _Primary Key_: one key defined by DBA
- _Superkey_: 1st condition holds but 2nd may not
	- Is _SID_ a key for students? (Maybe, needs to be unique)
	- What about name? (not a key or superkey)
	- Is {sid, gpa} a superkey? (maybe or maybe not)


- A table can have many candidate keys (specified using UNIQUE), but only
one primary key. 
• “Given a student and a course in Enroled1, there is a single grade.”
• What are other (implicit) constraints in Enroled1 and Enroled2?

```sql
CREATE TABLE Enroled1  
(sid CHAR(8),  
cid CHAR(8),  
grade CHAR(2),  
PRIMARY KEY (sid,cid) );
```

```sql
CREATE TABLE Enroled2  
(sid CHAR(8),  
cid CHAR(8),  
grade CHAR(2),  
PRIMARY KEY (sid),  
UNIQUE (cid, grade) );
```

### Foreign Keys, Referential Integrity

- _Foreign key_ : Set of attributes in one relation that “refers” to a tuple in another relation; _a Foreign key must correspond to a key (primary or candidate) of the other relation_ (like a 'logical pointer').
	- E.g. _sid_ in Enrolled is a foreign key referring to _Students_: 
		- Enrolled(sid: char(8), cid: char(8), grade: char(2))
	- Referential integrity is achieved if all foreign key constraints are enforced, i.e., no dangling references.
	- Can you name a data model w/o referential integrity?

### Foreign key in SQL

- Only students listed in the Students relation should be  
allowed to enroll in courses.

```sql
CREATE TABLE Enrolled  
sid CHAR(8), cid CHAR(8), grade CHAR(2),  
PRIMARY KEY (sid,cid),  
FOREIGN KEY (sid) REFERENCES Students );
```
![[Pasted image 20230110115506.png]]
