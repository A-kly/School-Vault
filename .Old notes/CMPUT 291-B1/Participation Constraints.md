# Participation Constraints

Does every project have a supervisor?
- If so, this is a participation constraint: the participation of Projects in Supervises is said to be total (vs. partial).
	-  Single line: Partial participation (_no entity required from other side of relationship_)
	- Double line (or bolded): Total participation (_requires at least one from other side of relationship_)
![[Pasted image 20230112115551.png]]
SQL example:
```sql
CREATE TABLE Proj_Supervises (  
pid INTEGER,  
pname CHAR(20),  
budget REAL,  
eid CHAR(11) NOT NULL,  
since DATE,  
PRIMARY KEY (pid),  
FOREIGN KEY (eid) REFERENCES Employees
ON DELETE NO ACTION)
```

## Total vs Partial Participation

![[Pasted image 20230112120030.png]]
_Easy to address via key constraints (previous slides)_

![[Pasted image 20230112120100.png]]
_Key constraints alone do not help, we need to use CHECK constraints or other “tricks”... (more on this later)_