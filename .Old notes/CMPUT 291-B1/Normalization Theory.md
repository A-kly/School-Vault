# Limitations of [[The Entity-Relationship Model|Relational Database]] Design
- Provides a set of guidelines, does not result in a unique database schema  
- Does not provide a way of evaluating alternative schemas  
- Pitfalls:  
	- Repetition of information  
	- Inability to represent certain information  
	- Loss of information
*Normalization theory provides a mechanism for analyzing and refining the schema produced by an E-R design*

**Let’s go back to E-R for minute ...
You’re asked to design an ER model for a scenario where there are users who are identified by their SINs and for whom we know their address (street number, street name, city name and postal code)**
![[Pasted image 20230314115658.png]]

# Redundancy
Dependencies between attributes cause redundancy
- Ex. All addresses in the same street have the same postal code
![[Pasted image 20230314115742.png]]

# Redundancy and Other Problems
- Set valued attributes in the E-R diagram result in multiple rows  in corresponding table  
- Example: Person (SIN, Name, Address, Hobbies)  
	- A person entity with multiple hobbies yields multiple rows in table Person  
		- Hence, the association between Name and Address for the same person is stored redundantly  
	- (SIN, Hobby) is key of corresponding relation  
		- The relation Person can’t describe people without necessarily associating them with a hobby

## Example
![[Pasted image 20230314115937.png]]
# Anomalies
- Redundancy leads to anomalies:  
	- *Update anomaly*: A change in Address must be made in several places  
	- *Deletion anomaly*: Suppose a person gives up all hobbies. Do we:  
		- Set Hobby attribute to null? No, Hobby is part of primary key  
		- Delete the entire row? No, we lose other information in the row  
	- *Insertion anomaly*: Hobby value must be supplied for any inserted row since Hobby is part of key

## Decomposition
- Solution: use two relations to store Person information 
	- Person1 (SIN, Name, Address) 
	- Hobbies (SIN, Hobby)
![[Pasted image 20230314120323.png]]
- The decomposition is more general: people with hobbies can now be described  
- No anomalies:  
	- Name and address stored once  
	- A hobby can be supplied separately or deleted
# Normalization Theory
- Result of E-R analysis need further refinement  
- Appropriate decomposition can solve problems  
- The underlying theory is referred to as normalization and is based on functional dependencies (and other kinds, like multivalued dependencies)
## Example
![[Pasted image 20230314120921.png]]

# Functional Dependencies
![[Pasted image 20230314120946.png]]
- A *constraint* on a relation schema R is a condition that has to be satisfied in <u>every</u> allowable instance of R.
	- FDs must be identified based on semantics of application.
	- **Given a particular allowable instance r of R, we can check if it violates some FD f, but we cannot tell if f holds over the schema R!**
	- A key constraint is a special kind of functional dependency: all attributes of relation occur on the right-hand side of the FD:
		-  SIN → SIN, Name, Address

# Armstrong’s Axioms for FDs
*https://en.wikipedia.org/wiki/Armstrong%27s_axioms*

![[Pasted image 20230314121250.png]]
*Reflexivity: Y is subset of X then: X gives rise to Y*
*Augmentation: X gives rise to Y then: XZ gives rise to YZ*
*Transitivity: easy and fine*
## Soundness and Completeness
![[Pasted image 20230314121540.png]]
## Other rules
- Decomposition
	- If X → YZ then X → Y and X → Z
- Composition
	- If X → Y and A → B then XA → YB
- Union
	- If X → Y and X → Z then X → YZ
- Pseudo-transitivity
	- If X → Y and YZ → W then XZ → W

# Generating FD closure (F+)
![[Pasted image 20230316111006.png]]

## Attribute Closure
- Calculating attribute closure leads to a more efficient way of checking entailment
- The attribute closure of a set of attributes, X, with respect to a set of functional dependencies, F, (denoted *X+ (F)*) is the set of all attributes, A, such that X → A
	- *X+ (F1)* is not necessarily the same as *X+ (F2)* if F1 ≠ F2
- Attribute closure and entailment:
	- Algorithm: Given a set of FDs, F, then X → Y if and only if *X+ (F)* ⊇ Y
![[Pasted image 20230316112100.png]]
*Closure on right, attributes on left. We can get  right side from each attribute on left side*
![[Pasted image 20230316112226.png]]
*if there is a functional dependency where x is giving rise to y then the y must be included in the closure.*
![[Pasted image 20230316112728.png]]
# Normal Forms
- Each normal form is a set of conditions on a schema that guarantees certain properties (*relating to redundancy and update anomalies*)
- First normal form (*1NF*) is the **same as the definition of relational model** (relations = sets of tuples; each tuple = sequence of *atomic values*)

- Second normal form (*2NF*): **no non-key attribute is dependent on part of a key**; has no practical or theoretical value
- The two commonly used normal forms are third normal form (*3NF*) and **Boyce-Codd normal form (BCNF)**

## BCNF
![[Pasted image 20230316113025.png]]
## (non) BCNF Examples
![[Pasted image 20230316113054.png]]
## Redundancy
![[Pasted image 20230316113123.png]]
# From BCNF to Decomposition
- Goal: Eliminate redundancy by decomposing a relation into several relations in a higher normal form  
- Decomposition must be lossless: it must be possible to reconstruct the original relation from the relations in the decomposition  
	- We will see why shortly

# Decomposition into BCNF
![[Pasted image 20230316113316.png]]
*In green: if we cant have x -> y, make a table with everything except y and a table with just x and y*
*Like the original [[#Redundancy and Other Problems|redundancy solution]]*
![[Pasted image 20230316113751.png]]
# Lossless Schema Decomposition
![[Pasted image 20230316113856.png]]
*DONT LOSE INFO*
# Lossy Decomposition
![[Pasted image 20230316113919.png]]
*POSSIBLE LOSS OF INFO*
![[Pasted image 20230316115658.png]]
# Lossy Decompositions: What is Actually Lost?
![[Pasted image 20230316115726.png]]
# Testing for LosslessNess
![[Pasted image 20230316115909.png]]
## Example
![[Pasted image 20230316115958.png]]
# Normalization Drawbacks
- By limiting redundancy, normalization helps maintain consistency and saves space
- But performance of querying can suffer because related information that was stored in a single relation is now distributed among several relations
## Example
`Person (SIN, Name, Address, Hobby)  `
```sql
SELECT Name, Hobby  
FROM Person
```
*FAAAAAAAAAAAAAAAST*
**VS**
`PersonInfo (SIN, Name, Address)`
`PersonHobby (SIN, Hobby)`
```sql
SELECT PI.Name, PH.Hobby  
FROM PersonInfo PI, PersonHobby PH  
WHERE PI.SIN = PH.SIN
```
*SLOW*

# Denormalization
- **Trade-off**: Judiciously introduce redundancy to improve performance of certain queries
- *Potentially expensive JOINs are avoided*
- *If queries are asked more frequently data is updated, added redundancy might improve average performance*

***Look at exercise online***