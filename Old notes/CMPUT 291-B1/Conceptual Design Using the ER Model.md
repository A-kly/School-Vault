# Conceptual Design Using the [[The Entity-Relationship Model|ER Model]]

Design choices:  
- Should a concept be modeled as an entity or an attribute?  
- Should a concept be modeled as an entity or a relationship?  
- Identifying relationships: binary or ternary?

## Entity vs. Attribute

- Should _address_ be an attribute (of Students) or an entity (connected to Students by a relationship)?
	- Depends on (a) its use and (b) its relationship with other entities
		- is it an object that we want to keep information about (independent of Students)?  (**not really**)
		- does it participate in a relationship with an entity other than students?  (**maybe, probably not**)
		- are there many students with no addresses?  (**I hope not, no**)
		- can several students share the same address? (**yes, roommates**)
	- A positive answer (yes) to one or more of those questions implies address is better modeled as an entity.
![[Pasted image 20230117114509.png]]
Diagram 1:
- Impossible to work in the same department at the same time
	- Student ID and Department ID are the same, we would have <u>repeating primary keys</u> in the table, this is **not allowed**
	- Not able to be identified uniquely

Diagram 2:
- Can work in the same department at the same time
	- Primary key includes shift length, this means the SID and DID can be the same w/ shift times being the only change, this **is allowed**
	- able to be identified uniquely

## Binary vs. Ternary Relationships

Can we represent this using binary relationships?
![[Pasted image 20230117115436.png]]
***NO***
![[Pasted image 20230117115521.png]]
*We can't easily deal with the qty (quantity) attribute, if we tie it to parts, shit gets fucked up*

![[Pasted image 20230117115705.png]]
*This is clear to see that project r1 is being supplied by supplier s1 and provides 7 of part p1*

![[Pasted image 20230117115819.png]]
*Who is suppling parts to which project??*


- Now add the constraint: *each part is supplied by a unique supplier*.
	- Not possible. A key constraint on Parts would also mean each part can only be used in a single project!
![[Pasted image 20230117120003.png]]