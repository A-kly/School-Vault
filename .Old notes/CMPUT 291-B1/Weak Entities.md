	A *weak entity* models an entity which is “part-of” an *owner entity*, and it cannot be uniquely identified without the primary key of the owner entity.
- Relationship is one-to-many (one owner, many weak entities).  
- Weak entity set has total participation in the identifying relationship set.
![[Pasted image 20230112120644.png]]
```sql
CREATE TABLE Dep_Care (  
dname CHAR(20),  
age INTEGER,  
cost REAL,  
sin CHAR(11)  
PRIMARY KEY (dname, sin),
FOREIGN KEY (sin) REFERENCES Employees  
ON DELETE CASCADE)
```
_`ON DELETE CASCADE` means: When the owner entity is deleted, all owned weak entities must also be deleted_

![[Pasted image 20230112121026.png]]
<u>sno</u>: weak entity
bold arrow: total participation, **all sections belong to one course**
therefore
	One professor can teach multiple sections of a course.