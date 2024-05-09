Related to [[Data Organization on Disks]]
# Introduction

- Information in a database can be seen as a collection of records (tuples) arranged in a set of files (relations).
- Each record consists of a collection of data values, with each value made by one or multiple bytes (depending on its domain).
- In this context we assume that each relation is stored within a specific file.
- Depending on the types of operations in a query, deciding how to arrange records in a file is very important. 
- Goal: maximize performance. 
- Let us assume that a file requires a number of pages equal to F...

# Heap Files
- Rows appended to end of file as they are inserted
	- Hence the file is unordered
- Deleted rows create gaps in file
	- File must be periodically compacted to recover space

_Uses binary search and merge sort_

**Eg: Transcript Stored as a Heap File**
![[Pasted image 20230214111952.png]]
# Performance
- Assume a file contains _F pages_.
- **Inserting** a row:
	- Access path is scan:
		- if necessary, check for duplicates (_F page transfers_).
		- Insert the element in the last page: 2 page transfers (_1 page read + 1 page write_).
- **Searching** for a row:
	- Access path is scan
		- Avg. _F/2_ page transfers if tuple exists (_Average record is 1/2 the disk away to find_)
		- _F_ page transfers if tuple does not exist
- **Deleting** a row:
	- Access path is scan
		- Avg. _F/2+1_ page transfers if tuple exists (_Average record is 1/2 the disk away to find and 1 page transfer to delete_) 
		- _F_ page transfers if row doesn’t exist

_"Opening the fridge and closing it doesn't take any operations, looking in to the fridge (reading) takes 1 operation (page transfer) and putting the elephant in (writing) takes 1 operation (page transfer) closing the fridge is no operations"_

- Organization inefficient when a subset of rows is requested: F pages must be read (due to absence of ordering).

```sql
SELECT T.Course, T.Grade  
FROM Transcript T -- equality search  
WHERE T.StudId = 123456  

--OR

SELECT T.StudId, T.CrsCode  
FROM Transcript T -- range search  
WHERE T.Grade BETWEEN 2.0 AND 4.0
```

# Sorted File
- Rows are sorted based on some attribute(s), e.g., PKs (think of a phone book) 
	- Access path is binary search 
	- **Equality** or **range query** based on that attribute has cost _log2(F) to retrieve page containing first row_ (_time complexity of binary search_)
	- Successive rows are in same (or successive) page(s) and _cache hits_ are likely
	- By storing all pages on the _same track_, seek time can be minimized.  
- Examples – Transcript sorted on StudId :
```sql
SELECT T.Course, T.Grade  
FROM Transcript T  
WHERE T.StudId = 123456  


SELECT T.Course, T.Grade  
FROM Transcript T  
WHERE T.StudId BETWEEN 111111 AND 199999
```

# Maintaining Sorted Order
**Problem**: we want to insert a new record. After the correct insert position has been determined (*log2(F)* page transfers), inserting the new record requires, on average, *F/2 reads* and *F/2 writes* (shifting necessary to make space: one read, one write each). Worst case: **O(F)**.
- Partial Solution 1: Leave empty space in each page: fillfactor
- Partial Solution 2: Use **overflow pages** (chains). Disadvantages: 
	- Successive pages no longer stored contiguously 
	- Overflow chain not sorted, hence cost no longer log2(F)
**Overflow pages:**
![[Pasted image 20230214114857.png]]

# Sorted vs heap files

- Sorted files represent a good choice w.r.t. heap files when dealing with queries containing equality or range searches.  
- On the other hand, if a sorted file has to be updated very frequently, it may be more convenient to use an heap file.

# External sorting
Problem: how do we sort huge files?
- Cannot fit in main memory.
- External sorting: based on a two-step approach that relies on the use of both main memory and disk.
	- 1st step (partial sort): logically divide the file to sort into segments (runs) that can fit into a buffer of M pages in main memory.
		- load each run into the buffer; sort the run via some suitable algorithm (e.g., Quicksort); write the sorted run back to disk.  
		- If *F = # file pages* and *M = # buffer pages*, then 1 st step generates *ceiling(F/M)* sorted runs, each of size (up to) M. 
		- 1st step requires *2F* disk I/O operations.
		- ![[Pasted image 20230214115730.png]]
	- External sorting, 2 nd step (k-way merge):
		- buffer in main memory holds M pages. Then we can linearly scan K=M-1 runs at once, and use the remaining page to flush the merged sorted run to disk. 
		- Takes advantage of the fact that runs are sorted.
		- ![[Pasted image 20230214115835.png]]
		- Starting from the initial N sorted runs (each of size (up to R) pages), iteratively call the merge step until we get the final sorted file. 
			- Each time merge step is invoked, the number of sorted runs gets reduced by a factor of K.
			- merge step called ceiling(log K N) times. 
		-  Overall I/O cost bounded by 2F * log K N

# Index (like a hash table)
![[Pasted image 20230214120038.png]]
- Intuition: [[Tree-Structured Indexes|index]] at the end of a book.
- Mechanism for efficiently locating row(s) without having to scan entire table.
- Don’t confuse candidate key with search key:
	- Candidate key: set of attributes; guarantees uniqueness
	- Search key: sequence of attributes; does not guarantee uniqueness – just used for search!

## Index Properties
Index entries:
- *Full record* vs *key and a pointer*
- *Integrated* vs *separate*
- *Clustered* vs *unclustered*
- *Dense* vs *sparse*

## Integrated Storage Structure
![[Pasted image 20230214120156.png]]
*Full record, Hash map gives you a FULL COPY of the record*
# Index File With Separate Storage Structure
![[Pasted image 20230214120446.png]]
_Hash map provides pointer to the location of the record_

# Clustered Integrated Index
![[Pasted image 20230214120528.png]]
*Hash map can return a RANGE of records*
# Clustered Separate Index
![[Pasted image 20230214120649.png|300]]
# Unclustered Separate Index
![[Pasted image 20230214120706.png|300]]
# Sparse Vs. Dense Index
![[Pasted image 20230214120726.png]]
# Exercises
![[Pasted image 20230214120841.png]]
![[Pasted image 20230214120908.png]]
![[Pasted image 20230214120924.png]]
![[Pasted image 20230214120936.png]]


**NEXT CLASS HAS A QUESTION ON MIDTERM ON IT**