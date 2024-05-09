Used in [[Database tuning]] and relates to [[Data Organization on Files]]
- Given a search key, is it possible to devise an index where entries can be located with a constant amount of page accesses?
- Goal: support equality searches in one disk access.
- Hash indexes: index having location mechanism based on some hash function + hash table.
# Hash Index - Overview
![[Pasted image 20230314110320.png]]
# Hash Function
![[Pasted image 20230314110348.png]]
*Input should be a primary key or another singular unique value, NOT a set value attribute. It depends!*
## Example
![[Pasted image 20230314110408.png]]
## More Hash Functions
![[Pasted image 20230314110444.png]]
![[Pasted image 20230314110524.png]]
![[Pasted image 20230314110539.png]]
![[Pasted image 20230314110604.png]]
# Choice of Hash function
![[Pasted image 20230314110758.png]]
## Conceptual example
![[Pasted image 20230314110830.png]]
# A Hashing Function
1. Convert the key to a number (if it is not)
	- key → K
2. Compute an address from the number
	- address = K mod M
	- Suggestion: Choose M to be a prime number (rationale: neutralize patterns in case the distribution of keys isn’t uniform).

# Collisions
- Problem: key is mapped to a bucket that is full. Where to store the overflow key?
- Static methods: size hash table remains constant.
	- Linear probing
	- Double hashing
	- Separate overflow
- Dynamic methods: hash table can grow or shrink.
	- Extendable hashing
	- Linear hashing
# Linear Probing

![[Pasted image 20230314112738.png]]
*Insert data into next space if we have a collision. If we fill the table completely, we have BIG PROBLEM*
*Key is stored with the value so if we have a collision we can identify the one we want*
## Problems
- Performance degradation as more rows are added: on average, need to access more pages when inserting/searching for an entry.  
- Waste of space as more rows are deleted.  
- Problems common to all static methods  
- Solutions  
	- Reorganization  
	- Use a dynamic method
# Extendable Hashing
![[Pasted image 20230314113724.png]]
# Summary
- An *equality search* on average takes only *1 disk access*
- *Range* search is *not supported*.
	- Since adjacent elements in range might hash to different buckets
	- *can't get a range of values*
- Partial key search is *not supported*.
	- Entire key must be provided
- **Not supported in SQLite.**
	- Supported in other DBMSs, e.g., Oracle and IBM DB2.

# Examples
## 1
```sql
SELECT E. Id  
FROM Employee E  
WHERE E.Salary < :upper AND E.Salary > :lower
```
- We have a range search on Salary.  
- Suppose the primary key is Employee.id; it is likely that there is a clustered index on that attribute.  
- Best option to maximize query performance?
	- Integrated clustered index is of no use for this query.
	- Use a secondary, B + tree index with search key Salary

## 2
```sql
SELECT T.StudId  
FROM Transcript T  
WHERE T.Grade = :grade
```

- We have an equality search on Grade.
- Suppose the primary key of Transcript is (StudId, Semester, CrsCode); it is likely that there is a main, clustered index on these attributes.
- Best option to maximize query performance?
	- Main index is of no use for this query.
	- Choose a secondary, B+ tree or hash index with search key Grade.

**More examples online**

