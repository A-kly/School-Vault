- Simple and powerful querying of data
	- Queries can be written intuitively, [[Databases#DBMS Functionality:|DBMS]] is responsible for 
	- Precise semantics for relational queries.  
	- Allows the optimizer to extensively re-order operations, and still ensure that the answer does not change.

>[!example]
```sql
	SELECT * /**(selects an entire row)*/
	FROM Students S /*(from students table)*/
	WHERE S.age=18 /*(where the student age is 18)*/
```

### Creating relations in SQL

- The type (domain) of each field is specified by user/programmer, and enforced by the DBMS (whenever tuples are added or modified)

>[!example]
```sql
CREATE TABLE Students  
(sid: CHAR(5),  
name: CHAR(10),  
login: CHAR(15),  
age: INT,  
gpa: FLOAT);  
CREATE TABLE Enrolled  
(sid: CHAR(5),  
cid: CHAR(10),  
grade: CHAR(2));
```

>[!example]
>Adding and deleting tuples
- Insert a single tuple:
```sql
INSERT INTO Students (sid, name, login, age, gpa)  
VALUES (11010, ‘Andrew’, ‘andrew@cs’, 18, 3.3);
```
- Delete all tuples that satisfy a condition (e.g., name =  Bob):
```sql
DELETE  
FROM Students  
WHERE name = ‘Bob’;
```

