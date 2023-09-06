# IsA Hierarchy

Consider forming a new entity set as the union of two or more entity sets
- Attributes and relationships common to all lower-level entity sets are moved to the higher-level entity set.
- **TOP of IsA relationship defines the Supertype**
![[Pasted image 20230117111632.png]]
- Also consider forming a derived entity set by taking a subset of a given entity set (_like a specialization of the entity_)
- Primary key of Graduates and Undergrads is _inherited_ from Students
- Students are like _Superclass_ and Graduates are like _Subclasses_ of that superclass

## Properties:
- Inheritance
	- Attributes of a supertype are attributed to subtype
	- Key of a supertype is key of subtype
	- Relationships of supertype are also relationships of subtype
		- eg. all students can be in a relationship with a class therefore, all Graduates and Undergrads can be in a relationship with a class
- Transitivity - Hierarchy of IsA
	- Undergrad student is a subtype of Student, student is a subtype of Person, so Undergrad is also a subtype of Person  (*a < b, b < c : a < c*)
- Reasons for using:
	- Makes ER diagram more concise and readable
	- Common attributes/relationships need not be repeated

## IsA Constraints

- *Covering constraints*: Does every Students entity also have to be a Graduates or an Undergrads entity? (default: no)
	- Graduates and Undergrads **cover** Students
- *Overlap constraints*: Can Joe be a Graduates as well as an Undergrads entity? (default: disallowed) (but possible)
	- Graduates **overlap** undergrads

## Mapping IsA Hierarchy

**General approach: _3 relations_**
- Students(sid, name)
- Graduates(sid, name)
- Undergrads(sid, name)

Example:
```sql
CREATE TABLE Undergrads (  
sid CHAR(8) NOT NULL,  
major CHAR(12),  
PRIMARY KEY (sid),  
FOREIGN KEY (sid) REFERENCES Students  
ON DELETE CASCADE)
```
_ON DELETE CASCADE_: removes Undergrad entry when Student and [[Keys & Key Constraints#Foreign Keys, Referential Integrity|foreign key]] is deleted
- Graduates and Undergrads DON'T _cover_ students
- May not be the most optimal, who knows tho

**Alternative: Graduates and Undergrads:**
- If Graduates and Undergrads DO _cover_ Students:
	- Graduates(sid, name, thesis)
	- Undergrads(sid, name, major)

- Only create 2 tables which are completely separated