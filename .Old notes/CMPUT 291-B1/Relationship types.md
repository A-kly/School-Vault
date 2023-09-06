# Relationship types
## Binary relationship Types: Many to many

**Constraints**: NONE
![[Pasted image 20230112113646.png]]
Employees can be in a relationship with many departments and vice versa
![[Pasted image 20230112113618.png]]
*[[Keys & Key Constraints#Foreign Keys, Referential Integrity|Foreign Keys]] are important so that we can keep data consistency, If someone quits, we need to restrict their ability to participate in relationship*


## Binary Relationship Types: Many-to-One

**Constraint**: each employee manages at most one department.
![[Pasted image 20230112114106.png]]
Given an employee, we can identify the one department they manage.
![[Pasted image 20230112114132.png]]
_Two different department IDs should never be associated with the same employee_
_Arrow indicates that source table allows only ONE entity from destination table_

## Binary Relationship Types: Many-to-One (alternative)

***Only change is Foreign key***
![[Pasted image 20230112114322.png]]
_Better in some aspects because_ #edit

## Binary Relationship Types: One-to-One

**Constraint**: each employee can manage at most one department and each department is managed by at most one employee.
![[Pasted image 20230112114525.png]]
_1 manages 2 departments, 76 is managed by 2 people_

**Look at syntax and examples in [slides](https://eclass.srv.ualberta.ca/pluginfile.php/9222404/mod_resource/content/1/Copy%20of%2003.ER%2BMapping_removed.pdf)**

## Ternary Relationships
![[Pasted image 20230112115206.png]]
*Meaning: Supplier s supplies part p for project r*
- Can we represent this using binary relationships?  
- Complication: add the Constraint “each part is supplied by a unique supplier for a unique project,”  
	- i.e., each part is in relationship with at most one supplier and one project.  
	- More on this later ...