# Set-Valued Attributes

Each employee can have one or more hobby.
- Attribute value can be a set (in contrast to the standard relational model)  
- E.g. (12345, Joe, (hockey, music))
![[Pasted image 20230112120213.png]]
Attributes **cannot** store more than one value  
- What is the key of the relation?  
- sin cannot be a key!
```sql
CREATE TABLE Employees (  
sin CHAR(11),  
name CHAR(20),  
hobby char(15),  
PRIMARY KEY (sin, hobby)
)
```
_sin and hobby are primary key because otherwise we end up repeating the same employee for each of their hobbies_

What about employees without any hobbies?