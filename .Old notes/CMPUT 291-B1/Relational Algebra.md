
# Relational Query Languages

- Languages for describing queries on a relational [[Databases]]  
- Three variants  
	- Relational Algebra  
	- SQL  
	- Relational Calculus (not covered in CMPUT 291)  
- Query languages vs. programming languages  
	- QLs not expected to be “Turing complete”.  
	- QLs support easy, efficient access to large data sets.

# SQL & Relational Algebra

- Relational Algebra
	- Immediate language used in [[Databases#DBMS Functionality:|DBMS]]
	- _Procedural_
		- The _how_
- Structured Query Language (SQL)
	- Predominant application-Level query language
	- _Declarative_
		- The _what_

## Algebra

- Study of operations in an abstract level on some domains
	- eg. operations _+, -, /,  *_ on natural numbers
- As a language, study of syntax and semantics of expressions
- Relational algebra
	- _Domain_: Set of all relations
	- _Expressions_: referred to as queries

## Relational Algebra

- _Basic Operators_:
	- select, project, union, set difference, cartesian product
- _Derived Operators_:
	- set intersection, division, join
- Procedural: combine queries for end result

## Role inside a DBMS

![[Pasted image 20230119113334.png]]
## Operators
**Relation IN = Relation OUT**
### Select Operator:
Select rows that satisfy a condition uses sigma: σ
![[Pasted image 20230119113512.png]]

- Operators: <, ≤, ≥, >, =, ≠  
- Simple selection condition:  
	- < attribute> operator < constant >  
	- < attribute > operator < attribute >  
- < condition > AND < condition >  
- < condition > OR < condition >  
• NOT < condition >


### Project Operator
Project on (or pick) a subset of columns
Uses Pi: π
![[Pasted image 20230119113941.png]]


#### Examples:
![[Pasted image 20230119114218.png]]

![[Pasted image 20230119114307.png]]
1. _Pick all people with hobbies of 'stamps' or 'biking' and then get id and name_
2. _Get id and name only from all people and then get those who have a hobby of 'stamps' or 'biking'_
	1. This will select no one, hobby field does not exist after pi

### Set Operations
- Relation = (roughly) a set of tuples
	- Set operations apply
- Operations:
	- ∩, ∪, − (set difference)
- Defined (or meaningful) between relations that have the same structure (called _union compatible relations_)

#### Union compatible relations

- Two relations are union compatible if:
	- Both have the same number of columns  
	- Names of attributes are the same in both  
	- Attributes with the same name in both relations have the same domain  
- Union compatible relations can be combined using union, intersection, and set difference

_`Person (SIN, Name, Address, Hobby)` and `Professor (Id, Name, Office, Phone)` are not union compatible, but `π name (Person)` and `π name (Professor)` are and `( π name (Person) - π name (Professor) )` makes algebraic sense_

### Cartesian Product

- R x S is the set of all concatenated tuples ( x, y ), where x is a tuple in R and y is a tuple in S
	- Relations don’t have to be union-compatible
- R × S can be very large (and expensive to compute) 
	- Factor of two in the size of each row 
	- Quadratic in the number of rows

![[Pasted image 20230119115612.png]]
### Renaming
- `expr [ A 1 , A 2 , ... A n ]`
	- expr returns a relation
	- Rename the first column in the result relation to A 1, the second to A 2, etc.
- Example
	- Let `R(a,b)` be a relation with two columns
	- `R[p,q]× R[r,s]` is a relation with 4 columns p, q, r and s.
- Common usage
	- To clean up the result
	- To prepare the result for the next operation

![[Pasted image 20230119115857.png]]
![[Pasted image 20230119115910.png]]

## Join (derived operator)

A (general or theta) join of _R_ and _S_ is the expression 
- R ⋈ (join condition) S
where join-condition is a conjunction of terms (Ai _oper_ Bi) and 
- Ai is an attribute of R;
- Bi is an attribute of S; and
- _oper_ is one of <, ≤, ≥, >, =, ≠
![[Pasted image 20230124110758.png]]

- **Problem**: If R and S have attributes with the same name, then the Cartesian product is not well-defined.
- *Two Solutions*:
	- Rename attributes prior to forming the product and use new names in join-condition
	- Common attribute names are qualified with relation names in the result of the join

### Example: 
![[Pasted image 20230124111634.png]]
![[Pasted image 20230124111653.png]]
### _Equijoin_:
Join condition is a conjunction of equalities.
![[Pasted image 20230124112319.png]]
### _Natural Join_:
Special case of equijoin:
- join condition equates _all_ and _only_ those attributes with the same name (condition doesn’t have to be explicitly stated) 
- duplicate columns eliminated from the result
Eg:
![[Pasted image 20230124112634.png]]
π (sid, Transcript.cid, Transcript.sem, grade, pid) ( Transcript ⨝ (Transcript.cid=Teaching.cid AND Transcript.sem=Teaching.sem) Teaching)

More generally:  
1. attr-list = attributes (R) ∪ attributes (S) (duplicates are eliminated)
	1. R ⨝ S = π attr-list (σ join-cond (R × S) )
2. join-cond has the form: A1 = A1 AND ... AND An = An  
3. {A 1 ... A n} = attributes(R) ∩ attributes(S)


### Example:

List the ids of students who took at least two different courses.

_Format_: Transcript(sid, cid, grade)

- Transcript ⨝ Transcript (?)
	- Renaming needed

![[Pasted image 20230124113417.png]]
_Student ID is the same, Course ID is different_

## Division

Finds tuples in one relation, r, that match all tuples in another relation, s
- `r (A 1  , ...A n  , B 1  , ...B m )`
- `s (B 1 ...B m )`
- r/s, with attributes `A 1 , ...A n`, is the set of all tuples `< a >` such that for every  
tuple `< b >` in s, `< a,b >` is in r

![[Pasted image 20230124114605.png]]
_Because relation s contains `a,b,c` and `2` and `3` are related to all of `a,b,c`, r/s contains only those in column A which are related to all of `a,b,c`_
_r/s contains all A where A is related to all of B_

![[Pasted image 20230124115204.png]]
_This all can be reduced to primitive operators as shows above_

Another example:
![[Pasted image 20230124115414.png]]
_To convert to primitive operations, find all students who have NOT completed all DB projects_

Primitive operations:
![[Pasted image 20230124120027.png]]

Steps:

1. Find all possible combinations of students and tasks (all tuples that could possibly be in Completed):
	1. ![[Pasted image 20230124120203.png]]
2. Of all possible tuples in T find the ones that do not exist in Completed in order to find students missing at least one task!
	1. U = T - Completed
3. Find the names of the students who are missing at least one task
	1. V = π Student (U)
5. Find the names of all students except the ones that are missing at least one task.
	1. W = π Student (Completed) − V

![[Pasted image 20230124120503.png]]
