# Database design process

When a very bad designer designs the database
- Bad shit happens

Make sure we get rid of data redundancy
![[Pasted image 20230112110844.png]]

# ER model

- Used to design conceptual schema
- The "world" is described in terms of
	- entities
		- eg. student ID
	- relationships
		- eg. a is _in_ b
	- attributes
		- eg. student: ID, name, major

_Entity_: a distinguishable object
- eg. name, place, thing
- represented as rectangle:
![[Pasted image 20230112112011.png]]

_Entity set_: a set of entities of the same type
- eg. courses

_Relationship_: represents the dact that certain entities are related to each other
- eg. John has taken CMPUT 291
- is it's own table:
|student|Class|grade|
|--------|------|-------|
|Jeff|Cmput291|B+|


_Relationship Set_: set of relationships of the same type.
- eg. students enrolled in course, cars registered to owners 
- represented as a dimond:
![[Pasted image 20230112111501.png]]

_Attribute_: describes a property of an entity or a relationship
- eg. student: id, name, major
- [[Keys & Key Constraints|Key]]: a minimal set of attributes that uniquely identifies each entity in an entity set (denoted by underlining such attribute names.)
- represented by oval (underline means primary key):
![[Pasted image 20230112111934.png]]

### Examples:
![[Pasted image 20230112112123.png]]

# ER Model Basics

Attributes of relationships:
- Students enrolled in course: year, semester, grade
- book on loan: loan date, due date
- Relationships NEVER have an originally unique primary key!
![[Pasted image 20230112112319.png]]
_Notice how the relationship can be many to many (three lines from race and from runner)_
_Relationship attribute is StartTime_

_Role_: the function of an entity set in a relationship set.
- Role labels are needed whenever an entity set has multiple functions in a relationship set
![[Pasted image 20230112112708.png]]
_Employee can be supervisor or subordinate, this changes who the report to in the Reports_To relation_






# Overview

Basics:  
- entities,  
- relationships,  
- attributes  
Additions:  
- [[Keys & Key Constraints|Key Constraints]]  
- [[Participation Constraints]]  
- [[Set-Valued Attributes]]  
- [[Weak Entities]]  
- [[Relationship types]]
- [[IsA Hierarchy]]

Make sure Constraints are understood well and are done correctly
ER diagrams are very subjective
